---
title: "PIXNET AppMarket 部落格文章編輯 Development README"
layout: post
date: "2012-08-29 15:46"
---

### PIXNET AppMarket 申請網址

<http://apps.pixnet.tw/appmarket> 以 PIXNET 帳號登入

### 建議參考範例

<https://github.com/manic/pixnet-js-addon/tree/master/youtube-embed-tool>

### 部落格文章編輯

- 點選[新增外掛](http://apps.pixnet.tw/appmarket/new)
- 服務選擇 _部落格文章編輯_，此時會看到 文章編輯 Addon 區塊出現

### IFrame Addon: Production

- Production 表示正式上線時所使用的環境
- Iframe URL: 使用的 iframe 用 url. 舉例: <http://tech.manic.tw/pixnet-js-addon/youtube-embed-tool/index.html?v=6>
- Proxy URL: 文章編輯類型 Addon 主要是利用 Iframe 方式來溝通，使用 [porthole](https://github.com/ternarylabs/porthole) 來實現 cross-domain iframe communication.
  - 範例: <http://tech.manic.tw/pixnet-js-addon/youtube-embed-tool/proxy.html> 建議可以直接將這個檔案的內容拿來做你的 proxy.html 
  - 注意: 要和你的 Iframe URL 是同一個 domain.

### 與 PIXNET 溝通

當 PIXNET 開啟這個APP頁面時, 會帶入參數, 以上述例子來說, 實際上在 PIXNET 頁面打開時，會類似下連結 <http://tech.manic.tw/pixnet-js-addon/youtube-embed-tool/index.html?v=6&addon_id=17&pToken=dd3c87f5488e3e0f315180880e536f23&proxy_url=//panel.pixnet.cc/addons/proxy&version=1.3&time=1346298936>  
要與 PIXNET 溝通，則也要打開 PIXNET 那方的 porthole。程式範例如下(也可參考原始碼)

    <script type="text/javascript">
    var windowProxy;
    $(function() {
        var proxy_url = $.query.get('proxy_url') + '?addon_id=' + $.query.get('addon_id') + '&pToken=' + $.query.get('pToken');

        windowProxy = new Porthole.WindowProxy( proxy_url );
        // Register an event handler to receive messages;
        windowProxy.addEventListener(function(event) { 
        });

        // 回傳訊息
        var ret = $.query.get('addon_id') + "||PIXNET||" + msg; //msg 表示你要回傳給PIXNET的資訊
        windowProxy.postMessage(ret); 
    });
    </script>

