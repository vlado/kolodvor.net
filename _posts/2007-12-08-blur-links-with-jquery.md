---
layout: post
title:  "Blur links with jQuery"
date:   2007-12-08 00:30:22 +0100
categories: javascript jquery
---

While surfing the Web, you probably noticed the dotted outline, that appears when you click on the link. If your link doesn’t lead to another page, but instead triggers some event in the same page, outline stays there and looks ugly.

For modern browsers you can remove it with simple css:

{% highlight css %}
a:focus, a:active {
  outline:none;
}
{% endhighlight %}

Unfortunately, this won’t do for IE 6 and earlier.

With jQuery it’s easy to get rid of the outline in every browser that has JavaScript enabled:

{% highlight javascript %}
$("a").click(function() {
  $(this).blur();
});
{% endhighlight %}

This will remove outline from the link once he is clicked. You will see the outline when clicking, but it will not stay there.

If you don’t want to se the outline at all replace click event with focus event:

{% highlight javascript %}
$("a").focus(function() {
  $(this).blur();
});
{% endhighlight %}

To find more about jQuery Events visit [http://docs.jquery.com/Events](http://docs.jquery.com/Events)
