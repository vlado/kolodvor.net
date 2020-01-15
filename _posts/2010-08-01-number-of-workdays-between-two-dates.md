---
layout: post
title:  "Number of workdays between two dates"
date:   2010-08-01 23:55:34 +0100
categories: ruby
---

It is pretty simple to get number of work days between two dates. For example we can get the number of workdays in this month.


{% highlight ruby %}
  start_date = Date.civil(2010, 8, 1)
  end_date = Date.civil(2010, 8, 31)
  workdays = (start_date..end_date).select { |day| ![0, 6].include?(day.wday) }.size
{% endhighlight %}

Please note that this doesn’t include any check for holidays, you’ll need to figure that yourself (if you have need for that at all).

For more info see [Array#select](http://ruby-doc.org/ruby-1.9/classes/Array.html#M000724) and [Date#wday](http://ruby-doc.org/ruby-1.9/classes/Date.html#M001468) methods.
