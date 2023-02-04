---
title: Ruby Select
layout: post
date: '2023-02-01 20:29:35'
categories: ruby
comments: true
---

This function of the Ruby Enumerable library is very simple. The select()
method is applied to an array or a hash. The job of select() is to select
elements that return true for a predicate applied to the element. (A predicate
is an expression that returns true or false, and it runs in the block passed
to select).
The following trivial example has the predicate always return true,
and therefore all members of the set are selected. In this case, the set is
[1,2,3,4,5] and the predicate is true:

{% highlight ruby %}
[1,2,3,4,5].select do |element|
   true
end
=> [1,2,3,4,5]
{% endhighlight %}

A slightly less trivial example selects even numbers (i.e., where the
predicate is **element % 2 == 0 ** ) from the original set of [1,2,3,4,5]:

{% highlight ruby %}
[1,2,3,4,5].select do |element|
   element % 2 == 0
end
=> [2,4]
{% endhighlight %}

Selects can be cascaded. Suppose you want to find the even numbers
between 1 and 100 starting with a 7. First, you select the even numbers.
Then, you select the numbers starting with a 7:


{% highlight ruby %}
irb>(1..100).select{|number| number % 2 == 0}\
irb*> .select{|even_number| even_number.to_s[0] == "7"}
=> [70,72.74,76,78]
{% endhighlight %}

You could also reverse the cascade:

{% highlight ruby %}
irb>(1..100).select{|number| number.to_s[0] == "7"}\
irb*> .select{|seven_number| seven_number % 2 == 0}
=> [70,72.74,76,78]
{% endhighlight %}

Since select returns an array, you can cascade select calls. For
example, you could have a select block select even numbers and then
square them using a map call. For example:

{% highlight ruby %}
[1,2,3,4,5].select do |number|
   number%2==0
end.map do |even_number|
   even_number * even_number
end
=> [4, 16]
{% endhighlight %}

A number of the more complex operations can be solved by cascading
with select calls.