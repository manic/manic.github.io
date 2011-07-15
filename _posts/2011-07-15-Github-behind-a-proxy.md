---
title: Github behind a proxy
layout: post
date: "2011-07-15 17:45"
---
### Environment

* Debian 6.0 (squeeze)

### Install corkscrew

    sudo apt-get install corkscrew

### Add config in .ssh/config

    Host github.com
      User git
      HostName ssh.github.com
      Port 443
      ProxyCommand corkscrew {proxy} {port} %h %p

### References

<http://petitesnouvelles.wordpress.com/2009/04/10/github-behind-a-proxy/>