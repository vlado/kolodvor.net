---
layout: post
title:  "Simple Search Rails plugin"
date:   2010-06-26 09:31:11 +0100
categories: ruby rails
---

SimpleSearch brings simple search to ActiveRecord. It ads simple_search named scope that accepts query as parameter.

The idea is that you provide the query and plugin does the rest (splits query to keywords and compose where statement).

This can be very useful in case you just want to filter list of records by some query, you have autocomplete field, … or something similar.

## Example

### View

{% highlight ruby %}
  <% form_tag request.path, :method => 'get' do %>
    <%= text_field_tag :query, params[:query] %>
  <% end %>
{% endhighlight %}

### Model

{% highlight ruby %}
  class User < ActiveRecord::Base
    acts_as_simply_searchable
  end

  # Columns: id, login, email, crypted_password, salt
{% endhighlight %}

### Controller

{% highlight ruby %}
  class UsersController < ApplicationController
    def index
      @users = User.simple_search(params[:query]).all
    end
  end
{% endhighlight %}

### Query examples

#### Simple query

{% highlight ruby %}
  User.simple_search("vlado")
  # => SELECT * FROM "users" WHERE (users.id LIKE '%vlado%' OR users.login LIKE '%vlado%' OR users.email LIKE '%vlado%' OR users.crypted_password LIKE '%vlado%' OR users.salt LIKE '%vlado%')
{% endhighlight %}

You can also provide :columns => :column1, :column2, … option to limit search only to those columns


{% highlight ruby %}
  class User
    acts_as_simply_searchable :columns => :login, :email
  end

  User.simple_search("vlado")
  # => SELECT * FROM "users" WHERE (users.login LIKE '%vlado%' OR users.email LIKE '%vlado%')
{% endhighlight %}

#### More complex query

{% highlight ruby %}
  User.simple_search("vlado, cingel")
  # will search for users matching 'vlado' and 'cingel' keywords
  # => SELECT * FROM "users" WHERE ((users.login LIKE '%vlado%' OR users.email LIKE '%vlado%') AND (users.login LIKE '%cingel%' OR users.email LIKE '%cingel%'))
{% endhighlight %}

**NOTE: With proper use of indexes this plugin can work quite well in most cases, but in case you have a large and complex database it is usually much better idea to use some search daemon like Thinking Sphinx.

More info at [http://github.com/cingel/simple_search](https://github.com/cingel/simple_search)
