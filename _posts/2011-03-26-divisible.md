---
layout: post
title:  "Divisible"
date:   2011-03-26 09:59:01 +0100
categories: ruby
---
I just published my first ruby gem on rubygems.org. It is a simple gem that is useful in case you need to find out if one number is divisible by another.

## Usage

{% highlight ruby %}
  9.divisible_by(3) # => true
  10.divisible_by(3) # => false
  12.divisible_by(3) # => true
  12.divisible_by(4) # => true
  15.divisible_by(4) # => false
{% endhighlight %}

Same can be done with

{% highlight ruby %}
  Divisible.check(9, 3) # => true
  Divisible.check(10, 3) # => false
  Divisible.check(12, 3) # => true
  Divisible.check(12, 4) # => true
  Divisible.check(15, 4) # => false
{% endhighlight %}

## Installation

{% highlight ruby %}
  gem install divisible
{% endhighlight %}

For more info go to [https://github.com/vlado/divisible](https://github.com/vlado/divisible)

