---
title: 'lets encrypt Nginx'
subtitle: ""
summary: ""

authors:
- admin

tags:

categories:

date: "2016-08-11"

featured: true
draft: false
math: true

# Featured image
# To use, add an image named `featured.jpg/png` to your page's folder.
# Placement options: 1 = Full column width, 2 = Out-set, 3 = Screen-width
# Focal point options: Smart, Center, TopLeft, Top, TopRight, Left, Right, BottomLeft, Bottom, BottomRight
image:
  placement: 2
  caption: "Credit -- Lets Encrypt"
  focal_point: ""
  preview_only: false

# Projects (optional).
#   Associate this post with one or more of your projects.
#   Simply enter your project's folder or file name without extension.
#   E.g. `projects = ["internal-project"]` references `content/project/deep-learning/index.md`.
#   Otherwise, set `projects = []`.
projects: []
---

Encrypting the web traffic is a standard practice today. It is used by almost everyone regardless of whether you are a Bank making sure your customers feel safe to use online services, an e-commerce website trying to gain the confidence of your customers or just another blog writer who wants to look cool with the nice green lock in the address bar. In today's world and with the recent developments/ enhancements in the TLS security (check the draft for v1.3 here [https://tlswg.github.io/tls13-spec/](https://tlswg.github.io/tls13-spec/)) and especially with the launch of [`Let's Encrypt`](https://letsencrypt.org/), there is only one reason to not encrypt your webtraffic.. Laziness! and No, encrypting all your traffic is not computationally heavy. So even if you are running your blog or any webservice on a $5/month 512MB droplet from digitalocean, you should be fine!

Anyways, so why did I make this move now? Call me stingy but I just cannot open my wallet to pay for services. However to my excitement, I got the [news](http://thehackernews.com/2016/03/lets-encrypt-free-ssl-certificate.html) about a new certificate authority [`Let's Encrypt`](https://letsencrypt.org/)which offers free SSL certificate! (well only 20 per domain per week but that's, frankly, quite enough!). Anyways thats was it for me.. Now, I HAD to do it. I decided to use the `Webroot` plugin. There are many other methods but I find this to be quite straightforward.

## What is Webroot?
Let's Encrypt provides a number of ways to obtain SSL certificates and install it for different webservers such as [`certbot`](https://certbot.eff.org/about/) which is a client tool to fetch and deploy the SSL/ TLS certificates based on the webserver that you are using. <br/>
[`Webroot`](https://certbot.eff.org/docs/using.html#webroot) is actually a plugin for the [`certbot`](https://certbot.eff.org/) which allows you to obtain the SSL certificate. The way it works is by placing a special file `.well-known` in the webserver's serving root location (like inside /usr/share/nginx/html/ or /var/www/html/. If you don't remember it then check the `/etc/nginx/sites-available/default` configuration file and look for where document `root` points to).

Installing the certificate, however, is left upto the user. <br/>
I use Nginx for serving all my web requests so this post is specifically for nginx. <br/>let's start with the process of encrypting all your web traffic. I am assuming you have: <br/>

- Root access to the server

- Have A record updated in DNS settings (check with your domain name provider like godaddy, namespace etc) and it correctly points to your server's ip address

- Some familiarity with Nginx and its configuration files

- Your favorite for a text editor (I use `emacs`.. so replace `emacs -nw` with your favorite text editor)

- Maybe a coffe, if you fancy

## Step1 : Installing Let's Encrypt
Best way, as of now, to get the Let's Encrypt client  is to clone the `master` branch from their github repository in root's home directory

```
~#> git clone https://github.com/letsencrypt/letsencrypt ~/
```

**OR**
another way would be to get a slightly old version using `apt-get` package manager

```
~#> apt-get install letsencrypt
```

## Step2: Nginx configuration for Webroot
Remember we talked about `.well-known` file that is used by Webroot plugin to validate the authenticity of your webserver? Lets put that in nginx configuration so that when Let's Encrypts services try to run the check, they should be able to see the file.

```
~#> sudo emacs -nw /etc/nginx/sites-available/default
```
and inside the server block add another location:

```
location ~ /.well-known {
                allow all;
	}
```

Reload nginx

```
~#> systemctl reload nginx
```

## Step3 : Obtaining SSL Certificate
Like I mentioned before, we will be using `Webroot` plugin to obtain SSL certificate

```
~#> cd letsencrypt
~#> ./letsencrypt-auto certonly -a webroot --webroot-path=/usr/share/nginx/html -d example.com -d www.example.com
```
> Replace example.com with your website name.
> certonly: only grab SSL certificate
> webroot: top-level root directory ("web root") same as what is configured in nginx's configuration file (`/etc/nginx/sites-available/defalt`)
> d: domain name

Answer the questions and in the end you should see a note which says something like:

```
IMPORTANT NOTES:
- If you lose your account credentials, you can recover through e-mails sent to your@email.com

- Congratulations! Your certificate and chain have been saved at
    /etc/letsencrypt/live/example.com/fullchain.pem. Your cert will expire on 2016-11-10. To obtain a new version of the certificate in the future, simply run Let's Encrypt again.

- Your account credentials have been saved in your Let's Encrypt configuration directory at /etc/letsencrypt. You should make a secure backup of this folder now. This configuration directory will also contain certificates and private keys obtained by Let's Encrypt so making regular backups of this folder is ideal.

- If like Let's Encrypt, please consider supporting our work by:
   Donating to ISRG / Let's Encrypt:   https://letsencrypt.org/donate
   Donating to EFF:                    https://eff.org/donate-le

```

> Make sure to note that the certificate that you received is only good for 90 days. After which you will have to run the script again. Hold on to that thought, we will talk more on that and write a script to automate this task for us :)
> Also note the location where the server's pvt key and certificates are generated. We will need them in next step

## Step4: Generate Diffie-Hellman Group
To strengthen the security even further, lets generate a nice 4096bit DH group which allows two devices to establish a shared secret over an unsecure communications channel.

```
~#> openssl dhparam -out /etc/ssl/certs/dhparam.pem 4096
```
> This might take a moment

## Step5: Nginx File Configurations:

Before we proceed, make a backup! (Not shown here)

```
~#> cp /etc/nginx/sites-available/default /etc/nginx/sites-available/default.bak
```

```
~#> emacs -nw /etc/nginx/sites-available/default
```

Now, assuming you have default configuration, make a server block on top of the existing server block. It should look like this:

```
server {
    listen 80 default_server;
    listen [::]:80 default_server;
    server_name example.com www.example.com;
    return 301 https://$server_name$request_uri;
    }

server {
       ... <your old stuff> 
       ...
       }
```

> Make sure to replace example.com with your website domain name

Now in the second server block, add these lines:

```
server {
       # SSL configs
       listen 443 ssl http2 default_server;
       listen [::]:443 ssl http2 default_server;
       ssl_certificate /etc/letsencrypt/live/example.com/fullchain.pem;
       ssl_certificate_key /etc/letsencrypt/live/example.com/privkey.pem;
       }
```

> Make sure to replace example.com with your website domain name

[`Cipherli.st`](https://cipherli.st/) provides a nice "suggested settings" for stronger security. Grab the information for nginx and put that in the second server block.<br/>
Finally, your configuration should look something like this:

```
server {
        isten 80 default_server;
       	listen [::]:80 default_server;
        server_name example.com www.example.com;
	return 301 https://$server_name$request_uri;
       }

server {
        # SSL configs
        listen 443 ssl http2 default_server;
        listen [::]:443 ssl http2 default_server;
        ssl_certificate /etc/letsencrypt/live/example.com/fullchain.pem;
        ssl_certificate_key /etc/letsencrypt/live/example.com/privkey.pem;

	# Forcing better security
	ssl_protocols TLSv1 TLSv1.1 TLSv1.2;
	ssl_prefer_server_ciphers on;
	ssl_ciphers "EECDH+AESGCM:EDH+AESGCM:AES256+EECDH:AES256+EDH";
	ssl_ecdh_curve secp384r1; # Requires nginx >= 1.1.0
	ssl_session_cache shared:SSL:10m;
	ssl_session_tickets off; # Requires nginx >= 1.5.9
	ssl_stapling on; # Requires nginx >= 1.3.7
	ssl_stapling_verify on; # Requires nginx => 1.3.7
	resolver <DNS-IP-1> <DNS-IP-2> valid=300s;
	resolver_timeout 5s;
	# Remove preloading!
	#add_header Strict-Transport-Security "max-age=63072000; includeSubDomains; preload";
	add_header Strict-Transport-Security "max-age=63072000; includeSubDomains;
	add_header X-Frame-Options DENY;
	add_header X-Content-Type-Options nosniff;

	# Adding DH group
	ssl_dhparam /etc/ssl/certs/dhparam.pem;
       }
```

> Remember to replace <DNS-IP-1> and <DNS-IP-2> with your preferred choice
> Also remember to disable preloading unless you know what you are doing
> Add DH group in the end

## Step 6: Almost done..
Restart nginx and check if it works

```
~#> systemctl restart nginx
```

## Step7: Auto Renewing!
It would be a pain to first of all remember to renew the certificate every 90 days and then making sure that I do! Instead what we'll do is set up a cronjob that will be triggered every Saturday at night 1am.

The command to renew the certificate is

```
~#> ./letsencrypt-auto renew
```
> If you run this now, you should see a message saying `No renewals were attempted` since we just installed the certificate.

Let's created a cronjob

```
~#> crontab -e
```

Following is the format for crontab

```
1. Entry: Minute when the process will be started [0-60]
2. Entry: Hour when the process will be started [0-23]
3. Entry: Day of the month when the process will be started [1-28/29/30/31]
4. Entry: Month of the year when the process will be started [1-12]
5. Entry: Weekday when the process will be started [0-6] [0 is Sunday]
```

So, if we want to schedule this task for every Saturday at 1am, the format should look like:
`0 1 * * 6`

the crontab entry would be:

```
0 1 * * 6 /root/letsencrypt/letsencrypt-auto renew >> /var/log/ssl-renew.log
5 1 * * 6 /bin/systemctl reload nginx
```
> Always reload nginx service so that new process is started first and then the old one is terminated. Restarting the nginx kills the old process first so it might happen that there was some error and your nginx server doesn't come back up!

That's **literally** it! You now have an encrypted web traffic to and from your server in just 7 steps! Enjoy
