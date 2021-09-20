---
title: 'Ruby for Rails: Blocks'
layout: post
date: '2018-01-30 12:06:31'
categories: ruby
comments: true
---

This post is the first in a series of blog posts about Ruby for Rails beginners. These are specifically for Rails developers who want to solidify their grasp of the Ruby language.

More than a decade ago, I started learning Rails before I knew any Ruby. Rails is written in Ruby of course, so when writing Rails code you are writing Ruby code. But at the beginning, I didn't fully understand how Ruby worked. And that's fine. A lot of people started learning Rails and picked up Ruby along the way.

The "Ruby for Rails" series will help you learn Ruby to make you a better Rails programmer.

In this blog post, we'll talk about blocks. Ruby blocks can be confusing to beginners but it's important that you learn them because you'll keep on using them on your Rails application.

One of the first code you'll see with blocks is with loops.

{% highlight ruby  %}
(1..10).each do |i|
  puts i
end
{% endhighlight %}

The block is inside <strong style="color: #C00;">do</strong> and <strong style="color: #C00;">end</strong>. This code displays the numbers 1 to 10. When you read it, it kind of makes sense. From 1 to 10, for each i, puts i. If you have experience with other programming languages, you might think this is just a more complicated way to do loops.

<strong style="color: #C00;">each</strong> isn't only for numbers. You can also iterate through an array.


{% highlight ruby  %}
["Alice", "Bob", "Eve"].each do |name|
  puts name
end
{% endhighlight %}


This code iterates through each element and prints the name. In Rails, you commonly use each when iterating through your model.

{% highlight ruby  %}
Post.all.each do |post|
  puts post.title
end
{% endhighlight %}

Say you have a Post model with a title. When you call  <strong style="color: #C00;">each</strong>  on  <strong style="color: #C00;">Post.all</strong> , you iterate on each of those posts and the value is assigned to **post **which is inside  `||` . Since <strong style="color: #C00;">post</strong>  is a Post object, you can call  <strong style="color: #C00;">post.title</strong>  inside the block.

The examples so far show that blocks can be used to iterate through some objects. But the iteration is a by product of the <strong style="color: #C00;">each</strong> method. Blocks aren't just for iteration. Here's another common code in Rails.

{% highlight ruby  %}
<%= form_with Post.new do |form| %>
  <%= form.text_field :title %>
  <%= form.text_area :body %>
<% end %>
{% endhighlight %}

We use <strong style="color: #C00;"><%%></strong>  because this code appears on ERB templates. form_with is used to display an HTML form. Here, we call the <strong style="color: #C00;">form_with</strong> method and passes the Post.new parameter. form_with yields an object which we assign to form. You can use any variable inside | |. We could have used f here instead of form.

In the examples above that used each, we yield each of the objects we're iterating through. In form_with, we yield exactly one object which is the FormBuilder associated with the model. Inside the block you can use FormBuilder's methods to generate fields like <strong style="color: #C00;">text_field, text_area, check_box, button,</strong>  etc.

All the fields inside the block are captured and displayed inside the HTML <strong style="color: #C00;">form</strong>  element.

These are just a few examples of blocks. You'll see more when writing Rails code. So don't get blocked out when coding!

I'd like this... original post by [https://www.engineyard.com/blog/ruby-for-rails-blocks](https://www.engineyard.com/blog/ruby-for-rails-blocks)