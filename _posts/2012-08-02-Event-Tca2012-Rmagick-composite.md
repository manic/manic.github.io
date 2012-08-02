---
title: "活動網站 tca2012 合成圖像(使用Rmagick)"
layout: post
date: "2012-08-02 12:40"
---

活動網站 [tca2012](http://tca2012.events.pixnet.net) 有一個功能要求是：選擇5位好友發出邀請，邀請上是一個照片包含自已與5位好友的頭像。

於是需要使用 Rmagick 來合成最多6張 Facebook 頭像與一張底圖。

事先已從 Art 那裡得到要合成的座標與圖片需要縮放的大小，這裡就寫一下 Rmagick 的部分。


### Debian(Ubuntu) 安裝 Rmagick 所需套件

    sudo apt-get install -y imagemagick libmagickwand-dev

### Gemfile

    gem 'rmagick'


### Rails code for composite

{% highlight ruby %}

class WelcomeController < ApplicationController
  def fbimage
    require 'RMagick'
    coordinates = [[28, 198], [47, 293], [136, 262], [225, 273], [315, 283]]
    img = Magick::Image::read("#{Rails.root}/public/fbimg.jpg")[0] #底圖
    img_from = Magick::Image::read("http://graph.facebook.com/#{params[:from]}/picture?type=normal")[0] #要合成的使用者頭像

    img = img.composite(img_from, 241, 127, Magick::OverCompositeOp) #使用 composite 來合成，241, 127指的是我要在這個位置合成它。
    tos = params[:to].split('-')
    tos.each_with_index do |to, index|
      next if to.to_i <= 0
      x, y = coordinates[index]
      img_to = Magick::Image::read("http://graph.facebook.com/#{to}/picture?type=normal")[0] #要合成的使用者朋友的頭像
      img = img.composite(img_to.resize_to_fit(70, 70), x, y, Magick::OverCompositeOp)
    end
    send_data(img.to_blob, :type => "image/jpeg", :disposition => "inline") #當做一般的 jpeg 來看待。
  end
end


{% endhighlight %}


