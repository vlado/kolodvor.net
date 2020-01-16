---
layout: post
title:  "Set focus on first field with jQuery"
date:   2008-01-17 18:50:41 +0100
categories: javascript jquery
---

If you are using PrototypeJS see [this](/javascript/prototypejs/2010/01/02/set-focus-on-first-field-with-prototype.html) post.

Setting focus on the first text field with jQuery is as simple as

{% highlight javascript %}
  $("input:text:visible:first").focus();
{% endhighlight %}

Find more at [http://docs.jquery.com/Selectors](http://docs.jquery.com/Selectors)
