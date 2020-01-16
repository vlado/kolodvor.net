---
layout: post
title:  "Radiant CMS, disable caching in development"
date:   2009-09-19 21:14:19 +0100
categories: ruby
---

I am working on extension for Radiant CMS. I wanted to disable caching for development, but wasn’t able to find right method for this, so finally I did it by putting this into my extensions activate method

{% highlight ruby %}
if RAILS_ENV=="development"
  Page.class_eval {
    def cache?
      false
    end
  }
end
{% endhighlight %}

This is more of a hack then a real solution, so please use comments to point me in the right direction. I’m using Radiant version 0.8.1.
