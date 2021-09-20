---
layout: post
title: "A silly idea to compare Jekyll vs Octopress"
date: 2017-06-07 11:16:07 -0300
categories: jekyll
comments: true
---

Before switching to Jekyll, I tried out Octopress, a blogging framework built on top of Jekyll....
I was really surprised to find out how much I disliked the experience with Octopress.
I had an impression that it is a hacker friendly, simple and extensible blog platform, but it was the opposite of that. There are many layers of abstraction, themes are pretty complicated, it comes with many ... pre-installed plugins out of the box, dozen depedencies (ruby gems), it uses Sass by default and so on. A fresh copy of Octopress blog consists of staggering 29 directories and 144 files it's too much..!!


Octopress works almost ok if you are willing to invest plenty of time to customize it or need to build something complex, but it wasn’t my particular use case. The complexity of Octopress defeats the whole purpose of a simple, generated static site. But you know what is “hacker friendly, simple and extensible blog platform”? That’s Jekyll! Jekyll is dead simple and practical. It was a pleasure to setup and customize the default theme. It took less than an hour to have a fully customized blog just the way I wanted. So I am staying with Jekyll this time. The directory structure is really simple and you start with the bare essentials, a simple layout and a CSS file. That’s it!

I tend to prefer simplicity and unix-like philosophy when it comes to choose every day tools for specific tasks. I can always extend, build and combine on top of that, when the time comes.

you can install jekyll with a simple command :

{% highlight ruby %}
$ gem install jekyll
{% endhighlight %}

Check out the [Jekyll docs][jekyll-docs] for more info on how to get the most out of Jekyll. File all bugs/feature requests at [Jekyll’s GitHub repo][jekyll-gh]. If you have questions, you can ask them on [Jekyll Talk][jekyll-talk].

[jekyll-docs]: http://jekyllrb.com/docs/home
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-talk]: https://talk.jekyllrb.com/
