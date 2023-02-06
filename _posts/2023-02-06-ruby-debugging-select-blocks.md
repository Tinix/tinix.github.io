---
title: Ruby Debugging Select Blocks
layout: post
date: '2023-02-06 21:23:05'
categories: ruby
comments: true
---

Debugging select is easy because the only thing you need to know is
whether the predicate was true for a particular element.
For example, a select filter that only keeps even numbers
(number % 2== 0) could be debugged like this:

{% highlight ruby %}
[1,2,3,4,5].select do |number|
  predicate = number % 2== 0
  puts "The predicate is #{predicate} for number #{number}"
  predicate
end
{% endhighlight %}

The predicate is false for number 1
The predicate is true for number 2
The predicate is false for number 3
The predicate is true for number 4
The predicate is false for number 5
=> [2, 4]

Here, you can see that only the numbers for which the predicate was
true ended up in the answer ([2,4]).


## FizzBuzz
This program is used as a programming question. Write a program to go
through a list of integers 1..N. If the number is divisible by 2, print “fizz”; if
it is divisible by 3, print “buzz”; if it is divisible by 2 and 3, print “fizzbuzz”;
otherwise, print the number.
The input can be modeled as a range: (1..15).

The output should look like this:

{% highlight ruby %}
1
fizz
buzz
fizz
5
fizzbuzz
7
fizz
buzz
fizz
11
fizzbuzz
13
fizz
buzz
{% endhighlight %}

{% highlight ruby %}
(1..15).map do |n|
if n % 2 == 0
   "fizz"
else
  n.to_s
  end
end
{% endhighlight %}

That gives us the following:


{% highlight ruby %}
=> ["1", "fizz", "3", "fizz", "5", "fizz", "7", "fizz", "9",
"fizz", "11", ... \ and so on
{% endhighlight %}

That is close, but we didn’t address the buzz:


{% highlight ruby %}
(1..15).map do |n|
if n % 2 == 0
   "fizz"
elsif n % 3 == 0
    "buzz"
else
   n.to_s
  end
end
{% endhighlight %}

That gives us the following:

{% highlight ruby %}
=> ["1", "fizz", "buzz", "fizz", "5", "fizz", "7", "fizz",
"buzz", "fizz", "11",\
"fizz", "13", "fizz", "buzz"]
{% endhighlight %}

That’s close, but the fizzbuzz examples didn’t happen at 6 and 12. Let’s
add in another clause. To be divisible by 2 and 3 implies that it must be
divisible by 6:


{% highlight ruby %}
fizzbuzz_list =
(1..15).map do |n|
   if n % 2 == 0
   "fizz"
elsif n % 3 ==0
   "buzz"
elsif n % 6 == 0
   "fizzbuzz"
else
   n.to_s
  end
end
{% endhighlight %}

This yielded the same result as the previous attempt. A closer
inspection of the code suggests that if the number is divisible by 6, it will
always be even and will be caught by the n%2==0 clause. However, if we
catch the n%6==0 clause first, what happens?

{% highlight ruby %}
fizzbuzz_list =
(1..15).map do |n|
  if n % 6 == 0
   "fizzbuzz"
elsif n % 3 ==0
   "buzz"
elsif n % 2 == 0
   "fizz"
else
   n.to_s
   end
end
{% endhighlight %}

That yields the following:


{% highlight ruby %}
=> ["1", "fizz", "buzz", "fizz", "5", "fizzbuzz", "7", "fizz",
"buzz", "fizz", "\
11", "fizzbuzz", "13", "fizz", "buzz"]
{% endhighlight %}

To print it, just do the following:

{% highlight ruby %}
fizzbuzz_list.each{|e| puts e}
{% endhighlight %}