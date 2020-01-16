---
layout: post
title:  "Stripe table rows with PrototypeJS"
date:   2009-09-16 21:35:30 +0100
categories: javascript prototypejs
---

I’ve spend a lot of time with PrototypeJS last few days, and this is going to be my first post related to prototype. So let’s see how to stripe the table using prototype, I think you will be surprised how easy it is.

HTML for our table will look like

{% highlight html %}
<table class="zebra">
  <thead>
    <tr>
      <th>Col1</th>
      <th>Col2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>11</td>
      <td>12</td>
    </tr>
    <tr>
      <td>21</td>
      <td>22</td>
    </tr>
    <tr>
      <td>31</td>
      <td>32</td>
    </tr>
  </tbody>
</table>
{% endhighlight %}

We will also need some CSS to change the background of the even rows and to highlight the row mouse is over

{% highlight css %}
table.zebra tr.even {
  background-color:#eee;
}
table.zebra tr:hover {
  background-color:#ccc;
}
{% endhighlight %}

And now all we need is as simple as

{% highlight javascript %}
$$('table.zebra tbody tr:nth-child(even)').each(function(tr) {
  tr.addClassName('even');
});
{% endhighlight %}

One thing to notice is that tr:hover selector won’t work in IE 6. If you care about IE6, solution could be to observe row for mouseover event and to add hover class dynamically.

You should add

{% highlight javascript %}
$$('table.zebra tbody tr').each(function(tr) {
  tr.observe('mouseover', function() {
    tr.addClassName('hover');
  }
});
{% endhighlight %}

and change table.zebra tr:hover to

{% highlight css %}
table.zebra tr.hover {
  background-color:#ccc;
}
{% endhighlight %}

Looks like this won’t be a last post devoted to Prototype 😉
