---
title: Ruby Debugging Map Blocks
layout: post
date: '2023-02-04 13:05:04'
categories: ruby
comments: true
---

The thing to remember is that map operates on each element of the
collection for each run of the block. When debugging, you want to see how
the block operated on each element.

{% highlight ruby %}
[1,2,3,4,5].map do |number|
  result = number* number
  puts "The result of the function on element: #{number} is #{result}"
  result
end
{% endhighlight %}


It is important to save the result in a local variable so that you can
return it as the last statement of the block. If you don’t, the result of the
puts statement will be returned (usually nil).