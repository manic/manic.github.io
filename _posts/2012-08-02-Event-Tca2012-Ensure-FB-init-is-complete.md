---
title: "活動網站 tca2012 製作心得－FB Async 與後續事件觸發"
layout: post
date: "2012-08-02 12:00"
---

參考 [How to detect when facebook's FB.init is complete](http://stackoverflow.com/questions/3548493/how-to-detect-when-facebooks-fb-init-is-complete)

使用 Facebook Javascript SDK 開發時，會有一個問題是：你必須確定 FB.init 已執行完畢後才繼續跑其他的 FB Javascript。

按照官方給的 script:

{% highlight javascript %}
  window.fbAsyncInit = function() {
    FB.init({
      appId      : 'YOUR_APP_ID', // App ID
      channelUrl : '//WWW.YOUR_DOMAIN.COM/channel.html', // Channel File
      status     : true, // check login status
      cookie     : true, // enable cookies to allow the server to access the session
      xfbml      : true  // parse XFBML
    });

    // Additional initialization code here
  };

  // Load the SDK Asynchronously
  (function(d){
     var js, id = 'facebook-jssdk', ref = d.getElementsByTagName('script')[0];
     if (d.getElementById(id)) {return;}
     js = d.createElement('script'); js.id = id; js.async = true;
     js.src = "//connect.facebook.net/en_US/all.js";
     ref.parentNode.insertBefore(js, ref);
   }(document));
{% endhighlight %}

所以會很自然的把所有 code 放在 window.fbAsyncInit 裡，FB.init() 底下。
但因為這對開發很不舒服，你會希望像是使用 $(function() 一樣，何時何地都可以確保你的 FB JS 程式碼保證在 FB.init() 之後執行。

做法是：


{% highlight javascript %}
  window.fbAsyncInit = function() {
    FB.init({
      appId      : 'YOUR_APP_ID', // App ID
      channelUrl : '//WWW.YOUR_DOMAIN.COM/channel.html', // Channel File
      status     : true, // check login status
      cookie     : true, // enable cookies to allow the server to access the session
      xfbml      : true  // parse XFBML
    });

    // 綁定在這之後會觸發 window.fbAsyncInit 
    $(window).triggerHandler('fbAsyncInit');
  };
{% endhighlight %}

接著只要想用 FB.api 時，就只要像這樣寫：

{% highlight javascript %}
$(window).bind('fbAsyncInit', function() {
  FB.api('...');
});
{% endhighlight %}

就可以確保會在 FB.init() 之後執行了。

在這次寫的活動網站 [tca2012](http://tca2012.events.pixnet.net) 就用到了這個技巧。