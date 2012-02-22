---
title: "Apache with Unicorn(Debian, Ubuntu, Rails)"
layout: post
date: "2012-02-22 17:20"
---

在參考[Installing on Ubuntu using Apache and Unicorn](https://github.com/teambox/teambox/wiki/Installing-on-Ubuntu-using-Apache-and-Unicorn)這篇文章後，試著在自家的 Server 這麼做，卻沒辦法成功。於是花了點時間修正這個 script.

### Step 1

    sudo a2enmod proxy
    sudo a2enmod proxy_balancer
    sudo a2enmod proxy_http
    sudo a2enmod rewrite

Restart Apache

    sudo /etc/init.d/apache2 restart

### Step 2

Install unicorn (maybe you can specify it in Gemfile)

    gem install unicorn

### Step 3

Start your unicorn server of your project, I use 2007 port instead 8080

    listen 2007 # by default Unicorn listens on port 8080, I use 2007 here.
    worker_processes 4 # this should be >= nr_cpus

### Step 4

The most important part in this post. 

    <VirtualHost *:80>

      ServerName example.org
      DocumentRoot /dir/of/your/project

      RewriteEngine On

      # Redirect all non-static requests to unicorn
      RewriteCond %{DOCUMENT_ROOT}/%{REQUEST_FILENAME} !-f
      RewriteRule ^/(.*)$ balancer://unicornservers%{REQUEST_URI} [P,QSA,L]

      <Proxy balancer://unicornservers>
        BalancerMember http://127.0.0.1:2007
      </Proxy>

    </VirtualHost>

_Important_: Dont use `ProxyPass / balancer://unicornservers/`, it will override rewrite rule.