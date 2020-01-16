---
layout: post
title:  "Create new app with specific Rails version"
date:   2010-02-25 12:09:50 +0100
categories: ruby rails
---

I recently installed Rails 3 beta release but I needed to create new app with the 2.3.5. version. I was searching for a way to do that and I found this

{% highlight ruby %}
  rails _2.3.5_ appname
{% endhighlight %}

Unfortunately this will produce an error similar to this

{% highlight ruby %}
  /usr/local/lib/ruby/site_ruby/1.8/rubygems.rb:827:in `report_activate_error': RubyGem version error: railties(3.0.0.beta not = 2.3.5) (Gem::LoadError)
	from /usr/local/lib/ruby/site_ruby/1.8/rubygems.rb:261:in `activate'
	from /usr/local/lib/ruby/site_ruby/1.8/rubygems.rb:68:in `gem'
	from /usr/local/bin/rails3:18
{% endhighlight %}

To fix this first run

{% highlight ruby %}
  which rails
{% endhighlight %}

and you will get a path to your rails executable, in my case this is /usr/local/bin/rails.

Then copy rails to rails3.

{% highlight ruby %}
  sudo cp /usr/local/bin/rails /usr/local/bin/rails3
{% endhighlight %}

Then open this file in your text editor (TextMate in my case).

{% highlight ruby %}
  mate /usr/local/bin/rails
{% endhighlight %}

and replace two last lines so that your file now looks like

{% highlight ruby %}
  require 'rubygems'

  version = ">= 0"

  if ARGV.first =~ /^_(.*)_$/ and Gem::Version.correct? $1 then
    version = $1
    ARGV.shift
  end

  gem 'rails', version
  load 'rails'
{% endhighlight %}

Thats it, now you can create your app with specific Rails version with

{% highlight ruby %}
  rails _2.3.5_ appname
{% endhighlight %}
