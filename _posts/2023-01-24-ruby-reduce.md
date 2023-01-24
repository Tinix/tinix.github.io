---
title: Ruby Reduce
layout: post
date: '2023-01-24 21:21:27'
categories: ruby
comments: true
---

This function of the Ruby Enumerable library is more complex than map()
and is quite powerful. The method is applied to a collection (for example,
an array or a hash). The job of reduce() is to apply a function cumulatively
to each member of the collection and then return an object (which could
be an array, a single value, a hash, or anything).

{% highlight ruby %}
[1,2,3,4,5].reduce(0, :+)
{% endhighlight %}


This is like saying for each member of the list, add (:+) the member to
memo and save the memo for the next element. The initial value of memo is 0
(the first parameter). Another way to code it is as follows:

{% highlight ruby %}
memo = 0
[1,2,3,4,5].each{|element| memo = memo.+(element)}
{% endhighlight %}

Or, you can pass reduce a block of code to run. The block comes after
the closing parenthesis and is surrounded by a do-end construct, or a {}
construct. The emitted variables are always the memo first and the element
second. (In this case, the initial value of memo is 33).

{% highlight ruby %}
[1,2,3,4,5].reduce(33) do |memo, element|
  memo.+(element)
end
memo
=> 48
{% endhighlight %}

(You don’t have to call them “memo” or “element,” but that is how they
behave). After each iteration, the memo takes the value of the last object in
the block. For example:



{% highlight ruby %}
[1,2,3,4,5].reduce(33) do |memo, element|
  memo.+(element)
  77.7
end
=> 77.7
{% endhighlight %}

This returned 77.7, because that was the last object in the block.
Another thing to remember is that the memo returned by the block has
to be of the same class as the memo emitted by the reduce function. For
example, when you are using reduce() to build a Hash object, you must
return the whole Hash object:

{% highlight ruby %}
[1,2,3,4,5].reduce({}) do |memo, element|
  memo[element] = element.to_s
end
{% endhighlight %}

IndexError: index 2 out of string
There is an error because the first run of the iteration returned
memo[element], which is a String class, but the input expects it to be a
Hash. To correct it, make sure that the memo of class Hash is explicitly the last
object returned, as follows:


{% highlight ruby %}
[1,2,3,4,5].reduce({}) do |memo, element|
  memo[element] = element.to_s
  memo
end
{% endhighlight %}

{% highlight ruby %}
=> {1=>"1", 2=>"2", 3=>"3", 4=>"4", 5=>"5"}
{% endhighlight %}


This worked because memo is a Hash class and was returned every time.
You can think of the reduce operation as operating on each element
and saving some kind of memo to carry forward to the operation on the
next element. In the preceding example, where you calculate the sum of
five numbers,

{% highlight ruby %}
[1,2,3,4,5].reduce(0,:+)
{% endhighlight %}

or

{% highlight ruby %}
[1,2,3,4,5].reduce(0) do |memo, element|
  memo + element
end
{% endhighlight %}

you are initializing the remembered quantity with a 0 and telling it to
remember to add the current element to the previously reduced quantity
and save it. The initial value of memo is an integer, and the last object
returned by the reduce block is also an integer.
You could remember other things in the memo too. For example,
you could save the last two numbers of a sequence. You would start with
an initial value of [nil,nil] for the last two remembered things. On every
iteration, you would push the element onto the memo (end of the array),
and then you would shift off the first element of the array.

{% highlight ruby %}
initial_memo = [nil,nil]
last_2 = (1..10).reduce(initial_memo) do |memo, element|
   initial_memo.push( element )
   initial_memo.shift
   initial_memo
end
=> [9,10]
{% endhighlight %}

In general, if you have to remember something about the previously
used elements when operating on the current element, use reduce(). If
you don’t need to remember anything, use map().
Sometimes reduce returns an array, in which case you can cascade it
with other reduce calls or map calls. For example, if you want to add the
sum of squares, you can use a map call to square each element, and then a
reduce call to add them. For example:


{% highlight ruby %}
[1,2,3,4,5].map do |number|
  number * number
end.reduce(0) do |sum, square|
  sum + square
end
=> 55
{% endhighlight %}

Or, perhaps you want to find the odd numbers of the last five in a
sequence:

{% highlight ruby %}
sequence = [1,2,3,455,5,6,4,3,45,66,77,54,23,4,55,6,7]
{% endhighlight %}


{% highlight ruby %}
sequence.reduce([nil,nil,nil,nil,nil]) do |memo, number|
  memo.push(number)
  memo.shift
  memo
end.select do |one_of_last_5|
  one_of_last_5%2 == 1
end
=> [23, 55, 7]
{% endhighlight %}

If this seems complex and idiomatic, don’t worry, because we’ll
explore these programming mechanics later in the blog. It suffices to say
that reduce can be used on both sides of a data-processing cascade. And
please always remember that the input memo must be of the same class or
structure as the output memo.