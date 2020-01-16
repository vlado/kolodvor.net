---
layout: post
title:  "Disabling sessions in Rails"
date:   2007-11-23 10:35:09 +0100
categories: ruby rails
---

The simplest way to disable sessions in Rails is to use `session :off` (see ActionController::SessionManagement::ClassMethods).

## session :off

To disable session suport only for a specific controller add `session :off` to that controller

{% highlight ruby %}
class MyController < ApplicationController
  session :off
end
{% endhighlight %}

Written like that, sessions are disabled for all actions on this controller.

Like filters, you can specify `:only` and `:except` clauses to restrict subset. The following code will disable session for first_action and third_action, but not for second_action.

{% highlight ruby %}
class MyController < ApplicationController
  session :off, :only %w(first_action third_action)

  def first_action
  end

  def second_action
  end

  def third_action
  end
end
{% endhighlight %}

Same could be achived with `session :off, :except => :second_action`.

The session options are inheritable, so to disable sessions for the entire application add `session :off` to ApplicationController.

{% highlight ruby %}
class ApplicationController < ActionController::Base
  session :off
end
{% endhighlight %}

## session :disabled => true

The downside of above approach is that if you disable sessions in ApplicationController with session :off you can’t enable them later on.

But luckily there is a cure for that. Instead of session :off add this line `session :disabled => true` to ApplicationController.

{% highlight ruby %}
class ApplicationController
  session :disabled => true
end
{% endhighlight %}

Now, you can re-enable session support in an inheriting controller with session :disabled => false.

{% highlight ruby %}
class MyController
  session :disabled => false
end
{% endhighlight %}

