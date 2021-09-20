---
layout: post
title: Install and config neotree on Emacs
dat: 2016-03-29 17:23:07 -0300
categories: FreeBSD, jekyll , programming, emacs
comments: true
---

Installation

Melpa

You can install the plugin using the packages on melpa.

Make sure you have something like the following in your Emacs startup file (~/.emacs.d/init.el, or ~/.emacs):

{% highlight ruby %}
    (add-to-list 'package-archives
                 '("melpa" . "http://melpa.org/packages/"))
{% endhighlight %}

To make that take effect, either evaluate that elisp expression or restart Emacs.

Then use M-x package-list-packages, select neotree from the list by pressing i, then press x to execute the changes. At that point, the package will be installed.

Source

Clone project:

{% highlight ruby %}
$ cd /some/path
$ git clone https://github.com/jaypei/emacs-neotree.git neotree
$ cd neotree
$ git checkout dev
{% endhighlight %}

Add config to emacs:

{% highlight ruby %}
(add-to-list 'load-path "/some/path/neotree")
(require 'neotree)
(global-set-key [f12] 'neotree-toggle)
{% endhighlight %}

Open (toggle) NeoTree:

{% highlight ruby %}
<F12>
{% endhighlight %}

Screenshots

{% include neotree.html
            img="images/neotree-1.png"
            title="emacs-neotree"
            caption="emacs-neotree is running!" %}
