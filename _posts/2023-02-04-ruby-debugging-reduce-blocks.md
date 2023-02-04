---
title: Ruby Debugging Reduce Blocks
layout: post
date: '2023-02-04 13:09:45'
categories: ruby
comments: true
---

Debugging reduce is a bit different because the memo is carried from
element to element. Therefore, you want to print out the element as well as
the memo.

{% highlight ruby %}
final_answer =
[1,2,3,4,5].reduce(0) do |memo, number|
  memo = memo + number
  puts "After operating on number: #{number}, the memo is #{memo.inspect} "
  memo
end
{% endhighlight %}

{% highlight ruby %}
After operating on number: 1, the memo is 1
After operating on number: 2, the memo is 3
After operating on number: 3, the memo is 6
After operating on number: 4, the memo is 10
After operating on number: 5, the memo is 15
{% endhighlight %}

Again, make sure that you save the memo before printing it, then
return it at the end of the block.
If you are using memo to build a different data structure as a part of
the reduce block, inspecting the memo becomes extremely useful in
converging on a good solution.