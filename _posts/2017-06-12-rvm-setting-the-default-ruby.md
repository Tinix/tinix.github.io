---
layout: post
title: "RVM Setting the default Ruby"
date: 2017-06-12 04:32:02
categories: ruby
comments: true
---

If you would like to make one specific Ruby be the default ruby that is selected when you open a new terminal shell, use the --default flag:

{% highlight ruby %}
$ rvm --default use 2.1.1

$ ruby -v

ruby 2.1.1p76 (2014-02-24 revision 45161) [x86_64-darwin12.0]

{% endhighlight %}

The next time you open a window Ruby 2.1.1 will be the selected ruby.

To switch back to your system ruby:

{% highlight ruby %}
$ rvm use system

$ ruby -v

ruby 2.0.0p451 (2014-02-24 revision 45167) [universal.x86_64-darwin13]
{% endhighlight %}

To switch at any time to the ruby you have selected as default:
{% highlight ruby %}
$ rvm default

$ ruby -v

ruby 2.1.1p76 (2014-02-24 revision 45161) [x86_64-darwin12.0]
{% endhighlight%}

To show what ruby is currently the selected default, if any, do:

{% highlight ruby %}
$ rvm list

rvm rubies

 * ruby-1.9.3-p484 [ x86_64 ]
   ruby-2.0.0-p481 [ x86_64 ]
=> ruby-2.1.1 [ x86_64 ]

# => - current
# =* - current && default
#  * - default

{% endhighlight %}

If you wish to switch back to your system ruby as default, remember that RVM does not "manage" the system ruby and is "hands off".

This means to set the "system" ruby as default, you reset RVM's defaults as follows.

{% highlight ruby %}
$ rvm reset
{% endhighlight %}

Note that "default" is merely implemented as an alias with an especially significant name.

If you encounter an error such as "RVM is not a function, selecting rubies with 'rvm use ...' will not work.", try using the alias action instead:

{% highlight ruby %}
$ rvm alias create default 2.1.1

{% endhighlight %}
