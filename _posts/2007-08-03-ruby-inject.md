---
layout: post
title:  "Ruby Inject"
date:   2007-08-03 22:19:33 +0100
categories: ruby
---

You probably frequently have to iterate through a list and accumulate a result that changes as you iterate. Let’s take the following array:

{% highlight ruby %}
nums = [1, 3, 5, 7]
{% endhighlight %}

If you want to find a sum of all the items in the array, you could write something like this:

{% highlight ruby %}
sum = 0
nums.each { |n| sum += n }
{% endhighlight %}

This works fine, but it doesn’t look much elegant. Luckly, for us that wants to be elegant there is a inject method.
(See: [Enumerable::inject](http://www.ruby-doc.org/core/classes/Enumerable.html#M003171))

{% highlight ruby %}
sum = nums.inject(0) { |x,n| x+n }
{% endhighlight %}

This code does the same thing, but also looks cool. Inject acomplish this by using accumulator or accumulated value (x). At each step accumulated value is set to the value returned by the block. Here, we set accumulator initial value to 0, and at each step current value from array (n) is added to accumulated value.

If initial value is omitted, the first item is used as the accumulator initial value and is then omitted from iteration.

{% highlight ruby %}
sum = nums.inject { |x,n| x+n }
{% endhighlight %}

Is same as

{% highlight ruby %}
sum = nums[0]
nums[1..-1].each { |n| sum += n }
{% endhighlight %}

Another example.
We have array with five names:

{% highlight ruby %}
names = ["michael", "ron", "scottie", "dennis", "toni"]
{% endhighlight %}

The following code:

{% highlight ruby %}
string = names.inject("") { |x,n| x << "#{n} " }
{% endhighlight %}

Will output:

{% highlight ruby %}
=> "michael ron scottie dennis toni "
{% endhighlight %}

You can get the same output with:

{% highlight ruby %}
string = ""
names.each { |n| string << "#{n} "}
{% endhighlight %}

Now, let’s say you won’t to separate them with comma, and capitalize those that have more then four characters.
You can do it like this:

{% highlight ruby %}
string = ""
names.each do |n|
  name = n.length > 4 ? n.capitalize : n
  n == names.last ? string << name : string << "#{name}, "
end
{% endhighlight %}

Or like this:

{% highlight ruby %}
string = names.inject("") do |x,n|
  name = n.length > 4 ? n.capitalize : n
  n == names.last ? x << name : x << "#{name}, "
end
{% endhighlight %}

In both ways we get the same result:

{% highlight ruby %}
=> "Michael, ron, Scottie, Dennis, toni"
{% endhighlight %}
