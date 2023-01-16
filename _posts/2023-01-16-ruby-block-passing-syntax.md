---
title: Ruby Block passing Syntax
layout: post
date: '2023-01-16 19:22:05'
categories: ruby
comments: true
---

Ruby is one of many languages that allow lexical closures, otherwise
known (kind of ) as anonymous functions or blocks. These functions are
dynamically created. The function can take the form of a defined function.
For example:

{% highlight ruby %}

irb> def plus_two(a,b)
irb>   a + b + 2
irb> end
irb> plus_two(3,4)
=> 9

{% endhighlight %}

Or, you could define it as follows:

{% highlight ruby %}
irb> plus_two = ->(a,b) do
irb>   a + b + 2
irb> end
{% endhighlight %}

Or, you could define it this way:

{% highlight ruby %}
irb> plus_three = ->(a,b){a + b + 3}
irb> plus_three.call(5,7)
=> 15
{% endhighlight %}


Now, anonymous functions or blocks can be passed to other functions
as parameters. A function that takes a function (defined or anonymous)
as a parameter will optionally execute the function in its program flow.
Suppose there is a function called printit() defined as follows:

{% highlight ruby %}
irb> printit = ->(a) do
irb>   puts a.inspect
irb> end
{% endhighlight %}

Now, suppose you want to print each element of a range. You will call
each on the array, which will run the block passed to each for each element
of the array.

{% highlight ruby %}
irb> (1..5).each(&printit)
1
2
3
4
5
=> (1..5)
{% endhighlight %}

You could also pass an actual block of code to run. The block is
surrounded by do and end or { and }. Objects between the vertical bars are
optionally passed to the block (depending on the definition of the block),
and they are used by the block to execute. The return value of a block is the
value of the last expression in the block.

{% highlight ruby %}
irb> (1..5).each do |num|
irb>   puts num.inspect
irb> end
{% endhighlight %}

You will get the same output as earlier. Ditto for the following:


{% highlight ruby %}
irb> (1..5).each{|num| puts num.inspect }
{% endhighlight %}

In Ruby, map, reduce, and select all take a code block as a parameter,
and the code block is executed as defined by the function