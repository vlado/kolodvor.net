---
layout: post
title:  "View man documentation in Preview"
date:   2010-02-12 09:12:12 +0100
categories: osx
---

If you are on OSX you can easily open man documentation using Preview. Just replace ls with command you would like to see documentation for.

{% highlight ruby %}
 man -t "ls" | open -f -a /Applications/Preview.app/
{% endhighlight %}

If you plan to do this often, you can make your life much easier by putting this inside your .bash_profile.

{% highlight ruby %}
 pman ()
 {
   man -t "${1}" | open -f -a /Applications/Preview.app/
 }
{% endhighlight %}

Now you can use following to view documentation in Preview


{% highlight ruby %}
 pman ls
{% endhighlight %}

Credit goes to [John W. Long](http://wiseheartdesign.com/articles/2010/02/12/my-current-toolset/).
