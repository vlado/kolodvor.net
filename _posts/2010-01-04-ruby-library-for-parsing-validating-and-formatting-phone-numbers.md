---
layout: post
title:  "Ruby library for parsing, validating and formatting phone numbers"
date:   2010-01-04 17:19:39 +0100
categories: ruby
---

[Tomislav Car](https://github.com/carr) has just released [Phone](https://github.com/carr/phone), Ruby library for phone number parsing, validation and formatting. It should save you a lot of time if you need any of the following:

* you have area where users input phone numbers in many different formats
* output phone numbers in specific format
* you need to send SMS messages from your app
* …

You can initialize new Phone object with Phone.new

{% highlight ruby %}
  Phone.new('5125486', '91', '385')
{% endhighlight %}

or

{% highlight ruby %}
  Phone.new(:number => '5125486', :area_code => '91', :country_code => '385')
{% endhighlight %}

Parsing is done using Phone.parse method

{% highlight ruby %}
    Phone.parse '091/512-5486', :country_code => '385'
    Phone.parse '(091) 512 5486', :country_code => '385'
{% endhighlight %}

It is smart to set default contry code first so you don’t have to provide it as option every time

{% highlight ruby %}
    Phone.default_country_code = '385'
    Phone.parse '091/512-5486'
    Phone.parse '(091) 512 5486'
{% endhighlight %}

~~Fow now, Phone works only for Croatian, Slovenian, Bosnian and Serbian phone numbers, but Tomislav is collecting data to support other countries.~~

[Go check it out](https://github.com/carr/phone)
