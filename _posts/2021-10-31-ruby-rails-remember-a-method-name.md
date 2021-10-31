---
title: Ruby remember a method name
layout: post
date: '2021-10-31 01:19:49'
categories: ruby
comments: true
---

Trying to remember a method name or just discover what you can call on an object? Ruby has you covered! Check out examples below

#### List all methods
{% highlight ruby %}

User.methods

{% endhighlight %}

#### List all direct methods except Object class methods
{% highlight ruby %}

User.methods - Object.methods

{% endhighlight %}

#### List all direct methods ( not comming from a parent class )
{% highlight ruby %}

User.methods(false)

{% endhighlight %}

#### List all instance methods
{% highlight ruby %}

User.instance_methods

{% endhighlight %}

#### List all direct instance methods
{% highlight ruby %}

User.instance_methods(false)

{% endhighlight %}

#### List all methods and then grep on them

{% highlight ruby %}

User.methods.grep(/find/)
=> [:find_for_database_authentication,
 :find_for_authentication,
 :find_first_by_auth_conditions,
 :find_or_initialize_with_error_by,
 :find_or_initialize_with_errors,
 :_find_callbacks,
 :_find_callbacks=,
 :after_find,
 :finder_needs_type_condition?,
 :find_by!,
 :cached_find_by_statement,
 :find_by,
 :initialize_find_by_cache,
 :find,
 :find_or_create_by,
 :find_or_create_by!,
 :find_or_initialize_by,
 :create_or_find_by,
 :create_or_find_by!,
 :find_each,
 :find_in_batches,
 :find_by_sql]

{% endhighlight %}