# sharmamohit.com-website

personal website hosted using AWS S3 at https://sharmamohit.com

###### Status:
![Website Status](https://img.shields.io/website-up-down-green-red/https/sharmamohit.com.svg?style=flat)
![Website Uptime](https://img.shields.io/uptimerobot/ratio/m781993530-436682a6e42e6d3bc06223b8.svg?label=Uptime&logo=clockify&style=flat)
[![Personal Website CICD](https://github.com/Mohitsharma44/sharmamohit.com-website/actions/workflows/build-site.yml/badge.svg)](https://github.com/Mohitsharma44/sharmamohit.com-website/actions/workflows/build-site.yml)

### Structure

The landing page on my website is a single index page in [`landing_page/index.html`](./landing_page)

The `/work/` slug is a portfolio website created using gohugo and Academic theme.

### Building

The website is built and deployed automatically by github workflows to AWS S3 bucket when a pull request is created. 
