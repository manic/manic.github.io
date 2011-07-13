---
title: "Active Record: 取出特定欄位不重覆的資料"
layout: post
date: "2011-07-13 15:39"
---

在翻程式碼的時候發現一段看起來怪怪的程式，研究了一下原本需求:

    在 notes 這個資料表中，取出最新 6 筆合法資料，其中 user 不得重覆
    notes belongs_to user

在原本的設計裡，是寫了一個迴圈，先去找最新一筆合法 note 的 user 資料，然後再去 note 問"不包含此 user 的最新一筆合法 note"
這個解法覺得不夠漂亮，於是研究了一下怎麼處理。

因為 user 要不重覆，所以很直覺得用 `group by user_id` 來做，但 group by 後的資料會沒辦法取得最新一筆。
和同事討教後才發現可以搭配 SQL 的 MAX(column) 和 GROUP BY。
最後整理成兩個 SQL，再回頭用 Active Record 生出我想要的 query code.

SQL 版本如下:

{% highlight sql linenos %}
SELECT MAX(`notes`.`id`) AS maximum_id, user_id AS user_id FROM `notes` WHERE `notes`.`is_valid` = 1 GROUP BY user_id ORDER BY maximum_id DESC LIMIT 6;
SELECT * FROM `notes` WHERE `id` IN (...);
{% endhighlight %}

Rails Code 如下:

{% highlight ruby linenos %}
rows = Note.where(:is_valid => true).group(:user_id).order("maximum_id DESC").limit(number_of_users.to_i).maximum(:id)
return Note.order('id DESC').find(rows.values)
{% endhighlight %}