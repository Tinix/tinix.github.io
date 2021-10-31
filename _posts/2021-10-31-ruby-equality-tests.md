---
title: Ruby Equality tests
layout: post
date: '2021-10-31 19:21:59'
categories: ruby
comments: true
---

The Object class defines three equality-test methods: ==, eql?, and equal?. At the Object level, all equality-test methods do the same thing: they tell you whether two
objects are exactly the same object. Here they are in action:


{% highlight ruby %}
>> a = Object.new
=> #<Object:0x00000101258af8>
>> b = Object.new
=> #<Object:0x00000101251d70>
>> a == a
=> true
>> a == b
=> false
>> a != b
=> true
>> a.eql?(a)
=> true
>> a.eql?(b)
=> false
>> a.equal?(a)
=> true
>> a.equal?(b)
=> false

{% endhighlight %}

All three of the positive equality-test methods give the same results in these examples: 
when you test a against a, the result is true, and when you test a against b, the result is false. (The not-equal or negative equality test method != is the inverse of the ==
method; in fact, if you define ==, your objects will automatically have the != method.)
We have plenty of ways to establish that a is a but not b.

##### But there isn’t much point in having three tests that do the same thing.
Further down the road, in classes other than Object, == and/or eql? are typically redefined to do meaningful work for different objects. For example, String redefines == and eql? to return whether the value of the strings being compared are identical. Two strings
can have the same value but in fact be different objects. The equal? method retains its Object definition and checks if two strings are exactly the same object. Let’s look at string equality in action:

{% highlight ruby %}
>> string1 = "text"
=> "text"
>> string2 = "text"
=> "text"
>> string1 == string2
=> true
>> string1.eql?(string2)
=> true
>> string1.equal?(string2)
=> false
{% endhighlight %}

As you can see, the strings are == and eql?, but not equal?. Ruby recommends against redefining equal? so that it can always be used to determine object identity.

Why do we have == and eql? if they’re synonymous at the Object level? Because it gives us more flexibility as we subclass Object. Because we don’t redefine equal?, we
have the option to redefine either == or eql? and compare objects in different ways.

For example, in the Numeric class (a superclass of Integer and Float), == performs type conversion before making a comparison but eql? doesn’t:

{% highlight ruby %}
>> 5 == 5.0
=> true
>> 5.eql? 5.0
=> false
{% endhighlight %}

Ruby gives you a suite of tools for object comparisons, and not always just comparison for equality.