---
title: "[工具]快速解決 “invalid multibyte char (US-ASCII)” Error (magic_encoding)"
layout: post
date: "2012-02-21 11:28"
---

在 ruby 1.9.x 系列，最常遇到的問題就是忘了補上 `# -*- encoding : utf-8 -*-` 導致 error
用 magic_encoding 這個 gem 可以快速解決這個問題

### Install

    gem install magic_encoding

### Usage

在 Rails 專案底下

    magic_encoding

就這樣，非常簡單

### References

[Github:magic_encoding](https://github.com/m-ryan/magic_encoding)
