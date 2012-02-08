---
title: Proxy settings in various RC files
layout: post
date: "2012-02-08 16:20"
---

為了要讓一台在防火牆內的機器能夠成功安裝 rvm 與 gem，奮鬥後的結果。

主要的問題在於有時候你不知道會出問題是因為 proxy 的原因，所以最好的方法是將你想得到的 rc 檔都加上 proxy 設定(如果有的話)

### gemrc

    gem: --http-proxy http://proxy.example.org:8080
    install: --no-rdoc --no-ri
    update: --no-rdoc --no-ri
    http-proxy: "http://proxy.example.org:8080"

### curlrc

    proxy = proxy.example.org:8080


### wgetrc

    http_proxy = http://proxy.example.org:8080
    use_proxy = on
    wait = 15

### cshrc

    setenv http_proxy 'http://proxy.example.org:8080'
    setenv HTTP_proxy 'http://proxy.example.org:8080'

### bashrc

    export http_proxy="http://proxy.example.org:8080/'