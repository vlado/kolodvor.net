---
layout: post
title:  "Set focus on first field with PrototypeJS"
date:   2010-01-02 15:32:02 +0100
categories: javascript prototypejs
---

If you are using jQuery see [this](/javascript/jquery/2008/01/17/set-focus-on-first-field-with-jquery.html) post.

To set focus on first text field with Prototype I prefer something like this

{% highlight javascript %}
  var firstField = $$('input:text:visible').first();
  if (firstField)
    firstField.focus();
{% endhighlight %}

but you can also try with [Form.focusFirstElement](http://api.prototypejs.org/dom/Form/focusFirstElement/) or [Form.findFirstElement](http://api.prototypejs.org/dom/Form/findFirstElement/)
