---
layout: post
title:  "Quick Start with Rails on OS X"
date:   2007-07-25 10:28:07 +0100
categories: osx rails
---

## Install Ruby

OS X (10.4) comes with Ruby 1.8.2 already installed.
For a quick start this is OK so let’s install Rails.

## Install Rails

Since Rails comes as gem package, first we need to install RubyGems.
Download the latest package from RubyForge and unzip it.
Now go to the directory where you unpacked the package and run

{% highlight shell %}
$ sudo ruby setup.rb
{% endhighlight %}

When asked enter your password, and after install finish you can verify that everything went well by typing:

{% highlight shell %}
$ gem -v
{% endhighlight %}

Output should look something like this, depending on version you installed

{% highlight shell %}
=> 0.9.4
{% endhighlight %}

Now installing Rails is as simple as

{% highlight shell %}
$ sudo gem install rails --include-dependencies
{% endhighlight %}

To verify installation, type:

{% highlight shell %}
$ rails -v
=> Rails 1.2.3
{% endhighlight %}

## Install MySQL

You can skip this step if you don’t want to use database but since Rails is a framework for developing database-backed web applications, you’ll probably want to use one.

1. Download the MySQL package for OS X for your platform
2. Double-click the drive image to mount it
3. Locate the MySQL installer (something like mysql-5.0.45-osx10.4-i686.pkg) and run it, authenticating as needed
4. Double-click MySQLStartupItem.pkg
5. Double-click MySQL.prefPane and install it

Once the install is complete, start the MySQL server using the control panel. ( System Preferences -> Other -> MySQL ) and check Automatically Start MySQL Server on Startup

## Test your installation

To start a new project (application), go to the directory where you plan to keep your applications (i.e. ~/Apps) and execute following commands

{% highlight shell %}
$ rails test_app
$ cd test_app
$ ./script/server
{% endhighlight %}

This will generate Rails skeleton in ~/Apps/test_app, and start a WEBrick server on port 3000.
Now open your browser and enter http://localhost:3000 in address bar. You should see a page with “Welcome aboard, You’re riding the Rails!” message.

We also need to tell Rails which database to use.
To do this edit database.yml file (~/Apps/test_app/config/database.yml) to look like this

{% highlight yaml %}
development:
  adapter: mysql
  database: test_app_development
  username: root
  password:
  host: localhost

test:
  adapter: mysql
  database: test_app_test
  username: root
  password:
  host: localhost

production:
  adapter: mysql
  database: test_app_production
  username: root
  password:
  host: localhost
{% endhighlight %}

Naturally we also need to create a database

{% highlight shell %}
$ mysqladmin -u root create test_app_development
{% endhighlight %}

and table in that database

{% highlight shell %}
$ mysql -u root
{% endhighlight %}

{% highlight shell %}
mysql> create table items (
         id INT NOT NULL AUTO_INCREMENT PRIMARY KEY,
         name VARCHAR(100) );
{% endhighlight %}

Execute scaffold command

{% highlight shell %}
$ script/generate scaffold item
{% endhighlight %}

Open http://localhost:3000/items and if you see something like this

{% highlight shell %}
Listing items

Name

New item
{% endhighlight %}

you have everything needed to get started with Rails development so Enjoy!
