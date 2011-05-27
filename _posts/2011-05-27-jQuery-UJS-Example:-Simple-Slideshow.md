---
title: "jQuery UJS 範例: Simple Slideshow"
layout: post
date: "2011-05-27 13:16:44"
---

原本程式碼

{% highlight erb %}
<div class="box-text">
<% events.each_with_index do |event, i| %> 
  <div class='grid <%= "mydiary-event-#{i+1}" %>'>
    <%= link_to(image_tag(event['img'], :size => "160x100"), event['link'], :target => "_blank") %> 
    <h3><%= link_to(event['title'], event['link'], :target => "_blank") %></h3>
    <p><%= event['description'] %></p>
    <span><%= duration(event['start_at'], event['end_at']) %></span>
  </div>
<% end %> 
</div>

<script type="text/javascript" charset="utf-8">
  $("#activity").find(".grid").hide();
  $("#activity").find(".mydiary-event-1").show();

  $(function(){
    var event_num = 1;
    var event_total = <%= events.size %>;
    $(document).everyTime("15s", function(i) {
      event_num = i % event_total + 1;
      $("#activity").find(".grid").hide();
      $("#activity").find(".mydiary-event-"+event_num).show();
    });
  });
</script>
{% endhighlight %}

可以看到這是一個客制化的特效，缺點是如果有別的 html block 要用同樣的特效，就得再為他寫上一段類似的程式碼。
於是參考 [jquery-ujs][] 的寫法來改寫。

改寫之後的原程式碼分成兩部分, 原來的 erb 與 獨立的 js

erb 區塊

{% highlight erb %}
<div class="box-text" data-simple-slideshow="true" data-second="15">
  <% events.each do |event| %> 
    <div class="grid">
      <%= link_to(image_tag(event['img'], :size => "160x100"), event['link'], :target => "_blank") %> 
      <h3><%= link_to(event['title'], event['link'], :target => "_blank") %></h3>
      <p><%= event['description'] %></p>
      <span><%= duration(event['start_at'], event['end_at']) %></span>
    </div>
  <% end %>
</div>
{% endhighlight %}

js 區塊(我是習慣放到 application.js)

{% highlight js %}
$(function() {
  // simple-slideshow
  $('div[data-simple-slideshow]').each(function() {
    var sec = parseInt($(this).data('second'));
    var $children = $(this).children();
    $children.hide().first().show();
    var size = $children.size();
    if ($().everyTime && size > 1) {
      $(document).everyTime(sec + "s", function(i) {
        $children.hide();
        $children.eq(i % size).show();
      });
    }
  });
});
{% endhighlight %}


[jquery-ujs]: https://github.com/rails/jquery-ujs