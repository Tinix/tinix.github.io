---
title: Ruby method missing
layout: post
date: '2023-01-05 23:54:32'
categories: ruby
comments: true
---

Method_missing is one of those special sauces that make Ruby such a
wonderful programming language. It acts like a catch-all method in a class - if
you call a method that the class doesn’t know how to respond to, Ruby will
first look for a method_missing method to handle this unexpected method
call. If method_missing doesn’t exist, then the typical NoMethodError will be
raised.
With method_missing, you can truly create dynamic classes that respond to a
wide variety of methods, based on things like database fields - Active Record
uses method_missing extensively to define getter and setter methods for
each of the fields in the model’s database table.
For an contrived example of method_missing in the flesh, you could define a
class like the following:

{% highlight ruby %}

class StringLength
   def method_missing(arg)
       "'#{arg}' has #{arg.length} letters!"
     end
end

{% endhighlight %}


And then interact with your class like so:

{% highlight ruby %}
> StringLength.new.a_word
=> "'a_word' has 6 letters!"
> StringLength.new.something_long
=> "'something_long' has 14 letters!"
> StringLength.new.does_it_respond_to_anything?
=> "'does_it_respond_to_anything?' has 28 letters!"

{% endhighlight %}

You probably won’t use method_missing extensively in your Rails apps, but
it’s good to know it exists, and the kinds of dynamic interfaces it can create.