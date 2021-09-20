---
layout: post
title:  "Problem solved with gem install libv8 on FreeBSD 10.2"
date:   2016-03-12 15:22:25 -0300
categories: jekyll, FreeBSD, gems. rubygems, libv8
comments: true
---

This is the output of running the command ‘gem install libv8’:

the result is :
…….
An error occurred while installing libv8 (3.16.14.13), and Bundler cannot continue.
Make sure that `gem install libv8 -v ‘3.16.14.13’` succeeds before bundling.

problem solved :

{% highlight ruby %}
sudo gem install libv8 -v '3.16.14.13' -- --with-system-v8
{% endhighlight %}

then

{% highlight ruby  %}
Building native extensions with: '--with-system-v8'
This could take a while...
Successfully installed libv8-3.16.14.13
Parsing documentation for libv8-3.16.14.13
Installing ri documentation for libv8-3.16.14.13
Done installing documentation for libv8 after 1 seconds
1 gem installed
{% endhighlight %}

and finally again running …bundle install

{% highlight ruby  %}
$bundle install
{% endhighlight %}
Hope that helps!

cheers Tinix!
