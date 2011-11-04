---
title: "安裝 Heroku Plugin: heroku-accounts"
layout: post
date: "2011-11-04 15:20"
---

現在公司也開始使用 [Heroku](http://www.heroku.com/) 為 hosting service 的工具，   
因為自己也有在使用 Heroku 的服務，   
於是切換 heroku account setting 就變得是一件擾人的事。

這時候就是 [heroku-accounts](https://github.com/ddollar/heroku-accounts) 這個 plugin 派上用場的時候了。


### 安裝，設定步驟

1. `heroku plugins:install git://github.com/ddollar/heroku-accounts.git`
2. `heroku accounts:add {自己的帳號} -auto` #加上 auto 可以自動設定好 .ssh/config，自己的帳號部分可以自由決定，並非指自己在 Heroku 上的帳號。我這裡是使用 manic
3. 會出現 `Enter your Heroku credentials.` 的提示訊息，輸入自己在 Heroku 上的帳號密碼
4. `heroku accounts:add work -auto` #加上公司帳號的資訊，加完後你會有兩組帳號可以使用 (work 可以換成任何英數組合名稱)
5. `heroku accounts:default {帳號}` #設定預設使用的帳號
6. (in heroku project path) `heroku accounts:set {帳號}` 設定此 project 使用的 heroku 帳號

### ~/.ssh/config

在你使用了 `heroku accounts:set work` 後，在你專案底下的 .git/config 檔裡會發現原本指向 heroku.com 的 repository url 變成了 `git@heroku.work:{repo}.git`，這是告訴 heroku 說你是要用 work 這個帳號管理這個 repo

而在 ~/.ssh/config 這個檔案裡會發現多了一段關於 heroku 的設定

    Host heroku.work
      HostName heroku.com
      IdentityFile /home/.ssh/identity.heroku.work
      IdentitiesOnly yes

這就是 heroku-accounts 使用的技巧。
