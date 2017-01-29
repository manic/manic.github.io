---
title: "Conditional scope in Rails"
layout: post
date: "2017-01-29 15:00"
---

### Case: conditional checking parameters in controller

考慮一個常見的 controller 程式碼片段：

{% highlight ruby %}
def index
  @products = Product.where(nil) # creates an anonymous scope
  @products = @products.status(params[:status]) if params[:status].present?
  @products = @products.location(params[:location]) if params[:location].present?
  @products = @products.starts_with(params[:starts_with]) if params[:starts_with].present?
end

# app/models/product.rb
class Product < ActiveRecord::Base
  scope :status, ->(status) { where(status: status) }
  scope :location, ->(location) { where(location: location) }
  scope :starts_with, ->(starts_with) { where(starts_with: starts_with) }
end
{% endhighlight %}

很驚人的是似乎有許多人都不知道 Rails model 的 scope block 允許回傳 `nil` 值

{% highlight ruby %}
class Product < ActiveRecord::Base
  scope :status, ->(status) { where(status: status) if status.present? }
end
{% endhighlight %}

如果傳入的 `status` 參數為 `nil`，則實際上會得到同等於 `where(:nil)` 的
`ActiveRecord::Relation`

所以我們可以將原本的 controller 重構為

{% highlight ruby %}
def index
  @products = Product.status(params[:status]).
    location(params[:location]).
    starts_with(params[:starts_with])
end

# app/models/product.rb
class Product < ActiveRecord::Base
  scope :status, ->(status) { where(status: status) if status.present? }
  scope :location, ->(location) { where(location: location) if location.present? }
  scope :starts_with, ->(starts_with) { where(starts_with: starts_with) if starts_with.present? }
end
{% endhighlight %}
