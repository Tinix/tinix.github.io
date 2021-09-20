---
layout: post
title: "Working with GREP in Ruby"
date: 2017-07-19 03:32:51
categories: ruby
comments: true
---
{% include grep.html
            img="images/grep.jpg"
            title="using GREP method in RUBY"
            caption="Using grep in RUBY..!!!" %}

As we know that ruby contains a lot of built in modules, in which one of this is the Enumerable module. So before preceddingon what GREP is and How it works, first lets study a little info about Enumerable module.

The Enumerable module provide us a lot of traversal and searching methods which also gives us the ability to do sorting.
This module basically provides us simpler methods to manipulate collections with the help of searching, traversing and sorting.
The class provides the each method which yields all the successive members of the collection.
Enumerable module is included in the class as follows:

{% highlight ruby %}
class dogs
  include Enumerable
  def breeds
    ..
  end

  ..
end
{% endhighlight %}

GRIP
First of all GREP is a powerful UNIX command.
GREP is a fantastic and a very useful method which comes along with the enumerable module in Ruby.
Using GREP is very handy and useful when it comes to manipulate collections instead of using a map or select methods.
Along with, Grep is very useful in customizing the filtering, lets see how we can customize the filters. Firstly, put the categorization logic as case equal("===") in a class once it is done after that the instance of that class will be easily filtered out from an Enumerable object using GREP method.
In the ruby methods of enumerable, we use “select” method for filtering and use “map” method for bulk transforming, but grep act as a combination of both these methods.

How does GREP work?
To filter the elements in an enumerable object most of the time Select method is usedand it is done by passing a block in it, lets see an example how it is done:

{% highlight ruby %}

["man", "van", "can", "dude", "pan", "fat"].select{|word| word.include?("an")}

{%  endhighlight %}

This is a result in

{% highlight ruby %}

["man","van","can","pan"]

{%  endhighlight %}

The same thing with less complicated code and syntax can be achieved with this very useful method GREP as follows

{% highlight ruby %}

["man", "van", "can", "dude", "pan", "fat"].grep(/an/)

{%  endhighlight %}


which will also return the same result as above but now with a less complicated code.
In the above example, what GREP did was it traversed through the array on which it was fired and it took out all the elements which had 'an' in them and gave us the resulting array.
Grep returns an array for each element in the enum in which the pattern is exactly equal to the elements passed in the array.
Grep works with regular expressions and all the other objects such as class and ranges.

Example of GREP are as follows:


{% highlight ruby %}
[2,20,200,2000].grep(2..200)
 # this will result in  
 # => [2, 20, 200]
{%  endhighlight %}


In the above example what grep did was it traversed through the array and picked up all the numbers between 2 to 200 and gave us the resulting array.

Lets see one more example

{% highlight ruby %}
[4,'a',5,'b',6,'c'].grep(Integer)
 # This will result in
 # => [4,5,6]
{% endhighlight %}

the same exampple for string :

{% highlight ruby %}
[4,'a',5,'b',6,'c'].grep(String)
 # This will result in
 # => ["a", "b", "c"]
{% endhighlight %}

and another example with join

{% highlight ruby %}
[4,'a',5,'b',6,'c'].grep(String).join
 => "abc"
[4,'a',5,'b',6,'c'].grep(String).join(',')
 => "a,b,c"
 {% endhighlight %}


In this above example what grep did was it pulled out all the integers from the main array on which we fired the method and gave us all the integers in the resulting array.
So, now I hope that the people reading this article would be through with what is GREP, How its used and how useful and handy it is when it comes to manipulate collections.

If you have any inputs or queries please feel free to post in comment section below
