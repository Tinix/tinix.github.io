---
title: Creating a random string on Rails
layout: post
date: '2017-09-26 00:49:08'
categories: ruby
comments: true
---

As we know that in almost all web applications we have to ammend functionalities in which we need to create a random string.
This string can contain some alpha numeric characters, numbers, lower case alphabets, upper case alphabets and etc.
This random string or token can be generated for many purposes like OTP ( one time password), recovery code etc.
Today we will see how to generate an eight character token with the help of arrays.
This token will have some numbers, upper case alphabets and lower case alphabets in all jumbled up manner.
Here is how we can do it...

{% highlight ruby %}
token = (('0'..'9').to_a + ('a'..'z').to_a + ('A'..'Z').to_a).shuffle.first(8).join
{% endhighlight %}

now as we can see we have taken a variable token in which we are storing numbers from 0 to 9
in the second bracket we have taken all the lower case alphabets.
in the third bracket we have taken all the upper case alphabets.
and converted them all into array through to_a method.
the plus sign concatenates all the arrays into one
then finally the .shuffle method will jumble up the whole string 
and first(8) method will take the first 8 characters from that jumbled up string hence giving us the required token.
Now everytime we will call this method it will generate a random string like this as seen in the picture below:

{% highlight ruby %}
2.2.5 :002 > token = (('0'..'9').to_a + ('a'..'z').to_a + ('A'..'Z').to_a).shuffle.first(8).join
 => "a9bIGCwP" 
2.2.5 :003 > token = (('0'..'9').to_a + ('a'..'z').to_a + ('A'..'Z').to_a).shuffle.first(8).join
 => "OZimKuqJ" 
2.2.5 :004 > token = (('0'..'9').to_a + ('a'..'z').to_a + ('A'..'Z').to_a).shuffle.first(8).join
 => "c09NCv8Z" 
2.2.5 :005 > token = (('0'..'9').to_a + ('a'..'z').to_a + ('A'..'Z').to_a).shuffle.first(8).join
 => "SyVPNqso" 
2.2.5 :006 > token = (('0'..'9').to_a + ('a'..'z').to_a + ('A'..'Z').to_a).shuffle.first(8).join
 => "mLhlOeQT" 
2.2.5 :007 > 
{% endhighlight %}


So I hope this blog was helpful to create a random string for multi purposes..!!