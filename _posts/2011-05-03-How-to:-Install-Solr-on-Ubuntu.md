---
title: 如何在 Ubuntu 下安裝 solr search engine
layout: post
time: "14:50"
---
### 版本資訊

* Ubuntu 11.04 (Natty)
* Solr 3.1
* JAVA (sun-java6)

### Install JAVA

    sudo add-apt-repository "deb http://archive.canonical.com/ natty partner"
    sudo apt-get update   
    sudo apt-get install sun-java6-jre sun-java6-plugin
    sudo update-alternatives --config java

### Install Solr

Download from here: <http://www.apache.org/dyn/closer.cgi/lucene/solr>

在此為了方便介紹, 會以個人身份而非 root 身份來安裝, 請根據個人狀況來調整。

    mkdir -p ~/solr
    cd ~/solr
    wget 'http://ftp.tc.edu.tw/pub/Apache//lucene/solr/3.1.0/apache-solr-3.1.0.tgz'
    tar xvfz apache-solr-3.1.0.tgz
    cd apache-solr-3.1.0/example

以下執行看要跑 single core 或是 multi core

    java -jar start.jar #default single core
    java -Dsolr.solr.home=multicore -jar start.jar

可以參考 apache-solr-3.1.0/example/README.txt

預設會跑在 http://localhost:8983
