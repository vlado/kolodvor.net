---
layout: post
title:  "Determining the number of days in a month"
date:   2007-08-22 11:18:20 +0100
categories: ruby
---

Here is a simple method that returns number of days for wanted month and year. If year is ommited current year is selected.

{% highlight ruby %}
def month_days(month, year=Date.today.year)
  mdays = [nil, 31, 28, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31]
  mdays[2] = 29 if Date.leap?(year)mdays[month]
end
{% endhighlight %}

Simple examples:

{% highlight ruby %}
month_days(1)       => 31
month_days(2, 2007) => 28
month_days(2, 2008) => 29
{% endhighlight %}

Now, let’s assume we have a date from a database, and we want to find number of days in a month from that date.

{% highlight ruby %}
month_days(date.month, date.year)
{% endhighlight %}

But with two more lines of code

{% highlight ruby %}
def month_days(date_or_month, year=Date.today.year)
  year = date_or_month.year if date_or_month.class == Date
  month = date_or_month.class == Date ? date_or_month.month : date_or_month

  mdays = [nil, 31, 28, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31]
  mdays[2] = 29 if Date.leap?(year)
  mdays[month]
end
{% endhighlight %}

we could find it like this:

{% highlight ruby %}
month_days(date)
{% endhighlight %}

It is worth mentioning that if String is passed as an argument

{% highlight ruby %}
month_days("2007-02-15")
{% endhighlight %}

we will get an ERROR, because first argument must be a Fixnum or a Date.

{% highlight ruby %}
month_days("2007-02-15".to_date)
{% endhighlight %}

If you want to use this as a helper in Rails, create the file date_helper.rb in a lib directory of your app, and put this in:

{% highlight ruby %}
module ActionView
  module Helpers
    module DateHelper

      def month_days(date_or_month, year=Date.today.year)
        year = date_or_month.year if date_or_month.class == Date
        month = date_or_month.class == Date ? date_or_month.month : date_or_month

        mdays = [nil, 31, 28, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31]
        mdays[2] = 29 if Date.leap?(year)
        mdays[month]
      end

    end
  end
end
{% endhighlight %}

and then add this line to config/environment.rb

{% highlight ruby %}
require lib/date_helper.rb
{% endhighlight %}

