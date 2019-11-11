---
layout: post
title:  "Webkit placeholder attribute behavior"
date:   2012-03-23 16:13:34 +0100
categories: javascript
---
As you probably notice, placeholder behavior has changed in the latest versions of Webkit (Safari and Chrome). If you don’t like it you can have old behavior back with a simple CSS rule

{% highlight javascript %}
input:focus::-webkit-input-placeholder, textarea:focus::-webkit-input-placeholder {
  color:transparent;
}
{% endhighlight %}
