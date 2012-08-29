---
title: "PIXNET AppMarket 部落格前台JS Development README"
layout: post
date: "2012-08-29 15:46"
---

### PIXNET AppMarket 申請網址

<http://apps.pixnet.tw/appmarket> 以 PIXNET 帳號登入

### 建議參考範例

<https://github.com/manic/pixnet-js-addon/tree/master/lightbox>

### 部落格前台JS

- 點選[新增外掛](http://apps.pixnet.tw/appmarket/new)
- 服務選擇 _部落格前台JS_，此時會看到 JS Addon 區塊出現

### JS Addon: Production

- Production 表示正式上線時所使用的環境
- Option Config: 此處用以表示提供給使用者的選項，使用格式為 JSON。 
  參考範例：<https://github.com/manic/pixnet-js-addon/blob/master/lightbox/options.json>
- Execute Code: 執行甪的程式碼, 並帶入 Option Config
  參考範例: <https://github.com/manic/pixnet-js-addon/blob/master/lightbox/execute.js>
- Script: 程式碼本體
  參考範例: <https://github.com/manic/pixnet-js-addon/blob/master/lightbox/script.js>

### JS Addon: Staging

- Staging 表示當 production 已有上線資訊時, 如需要更新版本, 可先寫在這裡以便測試與送審
- Staging Script Download URL: 表示 Script 可從何處取得. EX: <https://github.com/manic/pixnet-js-addon/blob/master/lightbox/script.js>
- Staging script Update Notifiation URL: 假設使用 github 做為你放檔案的工具, 那這段URL可以放置於 Repository Administration -> Service Hooks -> WebHooks URLS 裡, 
  這樣當你更新程式碼於 github 後, github 會透過這個 hook 告之 PIXNET 將你設定的 Staging Script Download Script 下戴並更新到你的 Staging Script.
