---
title: "擋外網的防火牆內的 Rails Server 如何透過 Proxy 連結外部網站"
layout: post
date: "2012-07-05 17:00"
---

在 Rails Server 必須放在內網且不允許直接外連時，當用到外部網站API時就會被擋下來。通常會拿到 `Errno::EHOSTUNREACH` 這種錯誤訊息。

解決方式是使用外部網站API時都要通過 Proxy 連出去，雖然可以在執行時指定，但每一次要連線就要做的話實在有點麻煩，所以就找了個可以一次設定的方法 -- [http\_configuration](http://rubygems.org/gems/http_configuration)

### Gemfile

    gem http_configuration

### config/initializers/env.rb

    ENV['http_proxy'] = 'http://proxy.srv.com:3128'
    ENV['NO_PROXY'] = 'localhost'
    Net::HTTP::Configuration.set_global(:proxy => :environment) if Rails.env.to_s != 'development'

### References

[Github:http\_configuration](https://github.com/bdurand/http_configuration)
