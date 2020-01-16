---
layout: post
title:  "MarkItUp: Rails plugin that turns any textarea into a markup editor"
date:   2010-07-05 17:14:09 +0100
categories: ruby rails
---

I recently published a plugin that helps you turn any textarea into a markup editor. It is based on excellent markItUp! jQuery plugin.

## Example

The most simple usage with preset defaults

{% highlight ruby %}
<html>
<head>
  <%= javascript_include_tag "path/to/jquery" %>
  <%= mark_it_up '#miu_test' %>
</head>
<body>
  <%= form_tag do %>
    <%= text_area_tag "miu_test" %>
  <% end %>
</body>
</html>
{% endhighlight %}

More info at [github.com/cingel/mark_it_up](https://github.com/cingel/mark_it_up)
