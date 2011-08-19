---
title: "Heroku app 的一些注意事項"
layout: post
date: "2011-08-19 10:52"
---

#### Ruby 版本

現在 Heroku 建立 App 時預設是使用 Ruby 1.9.2 <http://devcenter.heroku.com/articles/bamboo>
如果是像我這樣還在使用 REE 1.8.7 的話，就要在建立時指定好:

    heroku create --stack bamboo-ree-1.8.7

如果是已經建好 App 的話要改也是可以的:

    heroku stack:migrate bamboo-ree-1.8.7

#### Config

如果有用到像 Oauth 這種會需要 API key/password 的 gem, 那麼我們必須做好設定檔讓 Heroku App 正式上線時也能正常運作。  
而因為安全上的顧慮，我們不應該在 repository 裡將"密碼"放入，當然包含你的 API 帳號密碼  
Heroku 提供了 `heroku config:add #{KEY}:#{VALUE}` 的指令讓你能夠設定帳號密碼，然後你可以用在程式碼裡用 ENV['KEY'] 的方式存取。

參考：<http://devcenter.heroku.com/articles/config-vars>

#### 時區

這是最近發現的，可能算地雷。

Heroku App 其實不會完全吃 `config.time_zone = 'Taipei'` 這種時區指定，而是要用 `heroku config` 來指定:

    heroku config:add TZ=Asia/Taipei

然後你的時間操作才會完全正常，不然會像我一樣 Time.zone 回傳 Taipei 但時區卻是在 -0700 的詭異情況

參考: <http://stackoverflow.com/questions/2719330/heroku-time-zone-problem-logging-local-server-time>

#### Console

Heroku 同樣提供 console 介面: `heroku console`

參考: <http://devcenter.heroku.com/articles/console>

#### Backup

Heroku 同樣提供 backup addon，而且是免費的: `heroku addons:add pgbackups`

參考: <http://devcenter.heroku.com/articles/pgbackups>

### 個人用 Heroku App initial script

    heroku create --stack bamboo-ree-1.8.7
    heroku config:add TZ=Asia/Taipei
    heroku addons:add pgbackups

記一下免得下次又要重找。