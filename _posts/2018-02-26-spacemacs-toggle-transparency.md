---
title: spacemacs toggle-transparency
layout: post
date: '2018-02-26 19:01:21'
categories: spacemacs
comments: true
---

Anything added via spacemacs/add-toggle or things available in SPC t and SPC T should be proper toggles. This way, you can toggle them in user-config if you want to change the default state.

Specifically, spacemacs/toggle-transparency (and the related spacemacs/toggle-transparent-frame) both open a micro-state (in addition to toggling the setting). This means, that, if you want to have a transparent frame by default, you cannot just add (spacemacs/toggle-transparency) to your .spacemacs, because it will open the micro-state instead of just toggling transparency.

I'm not sure what other toggles do this, if there are any at all.

Ah, for now, I'm using this code in my user-config as a workaround:

{% highlight ruby  %}
 ;; Transparency by default
  (set-frame-parameter (selected-frame) 'alpha
                       (cons dotspacemacs-active-transparency
                             dotspacemacs-inactive-transparency))

{% endhighlight %}

later , spacemas reload config 

SPC f  e  R 

if you want load theme 

SPC T s and select theme and enter