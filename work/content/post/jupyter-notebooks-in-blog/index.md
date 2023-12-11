---
title: 'Jupyter notebooks in blog'
subtitle: "for static website builders and blogging platforms that don't support this natively"
summary: "I love Jupyter notebooks! They are great for experimenting and playing around with the ideas. I always liked the idea of using a single web based application for writing code snippets, visualizations, creating presentations and even blogging!"

authors:
- admin

tags:
- jupyter
- blog
- python

categories:
- tutorial
- python

date: "2016-07-12T00:59:02-04:00"

featured: true
draft: false
math: true

# Featured image
# To use, add an image named `featured.jpg/png` to your page's folder.
# Placement options: 1 = Full column width, 2 = Out-set, 3 = Screen-width
# Focal point options: Smart, Center, TopLeft, Top, TopRight, Left, Right, BottomLeft, Bottom, BottomRight
image:
  placement: 2
  caption: ""
  focal_point: ""
  preview_only: false

# Projects (optional).
#   Associate this post with one or more of your projects.
#   Simply enter your project's folder or file name without extension.
#   E.g. `projects = ["internal-project"]` references `content/project/deep-learning/index.md`.
#   Otherwise, set `projects = []`.
projects: []
---

I love Jupyter notebooks! They are great for experimenting and playing around with the ideas. I always liked the idea of using a single web based application for writing code snippets, visualizations, creating presentations and even blogging! <br/>
There are great static website generators out there but most of them use restructured text or markdown to convert to html pages.

Developers of jupyter notebooks have now embedded the nbconvert tool for converting notebooks (`ipynb`) to Markdown (`md`) or ReStructuredText (`reST`) and even standalone `html` with all the css stylings. Regardless of whether you use blogging engines like [`Wordpress`](https://wordpress.com/) or static website generators like [`Hugo`](https://gohugo.io/), the issue of formatting the notebook so that they play well with your website has always persisted.

## Using Jupyter notebooks in your blog
I've always had two options:

- Convert Notebooks to Markdown<br/>
Use Jupyter notebook's built-in command to convert to markdown and then spend 20 more minutes correcting formatting, image's that are embedded, code blocks, etc. I would then convert to html using [`Hugo`](https://gohugo.io/) or [`Pelican`](http://blog.getpelican.com/) website generator (based on what I am using for my website) and then publish it online.  Problem with this method? Formatiing, Code samples, Code coloring, everything lost!

- Convert Notebooks directly to html<br/>
Use Jupyter notebook's built-in command to convert to html and use it in my blog. Issues with this? Horrible CSS! Don't get me wrong. The html output from Jupyter's nbconvert was meant to provide a decent layout and styling for a standalone professional html file.. and it does that well. However if you are like me, you have some global layout style that you want your notebook in.

## Available Tools
I have used:

- [`pelican-ipynb`](https://github.com/danielfrg/pelican-ipynb) plugin for blogging using ipython (or Jupyter) notebook. However I had a hard time setting it up. Plus there were some incompatibilities with the themes that I was using. It is a good tool and you can check it out here: (https://github.com/danielfrg/pelican-ipynb) but I wanted something that would.. Just.. Work!

- [`Nikola`](https://getnikola.com/blog/) static website generator just like `Hugo` and `Pelican`. It has an added advantage that it supports blogging via notebooks right out of the box. Sweet! but it is really targeted at making a blog first that means main page always seems to be the blogroll. Whereas I wanted a single page academic website having my intro on top and publications and then posts with some kind of blogroll in there. Anyways it really felt targeted towards a blog site or a site with lots of posts. Moreover it uses [`Mako`](http://www.makotemplates.org/) templating engine whereas I was more familiar with [`jinja`](http://jinja.pocoo.org/) and [`Go` template library] (https://golang.org/pkg/html/template/). Anyways in the end, I decided to stick with either `Pelican` or `Hugo`

I have spent enough hours trying to google and reading forums to realize that there is no one tool to solve it all. In the end I decided to do this manually. I opened chrome developer tools and started analyzing the generated html page. <br/>
Stripping away as much css styling as possible, I was finally able to create a barebones version of css styling that can be used with the exported html page  (from notebook using nbconvert).
<br/>

Now whenever you want to embed your notebook in your blog, you can simply:

- Convert the jupyter notebook to basic html file:
```
jupyter nbconvert --to html --template basic *source_file.ipynb* *target_file.html*
```
- Download the [`jupyter.css`](http://sharmamohit.com/css/jupyter.css) file and place it in your css folder of your website.

- Now simply modify your base index html file or whatever it is that contains the boiler plate/ placeholder for your website by adding a css tag linking to this file.

That's it!
