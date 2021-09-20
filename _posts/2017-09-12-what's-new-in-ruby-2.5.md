---
title: What's new in Ruby 2.5?
layout: post
date: '2017-10-12 09:27:58'
categories: ruby
comments: true
---

# Ruby 2.5.0-preview1 Released

![useful image]({{ site.url }}/images/ruby.png)

We are pleased to announce the release of Ruby 2.5.0-preview1.

Ruby 2.5.0-preview1 is the first preview release toward Ruby 2.5.0. It introduces some new features and performance improvements, for example:

After installing the beta version through rvm ...

{% highlight ruby %}

 tinix   rvm install 2.5.0-preview1
Searching for binary rubies, this might take some time.
No binary rubies available for: debian/9/x86_64/ruby-2.5.0-preview1.
Continuing with compilation. Please read 'rvm help mount' to get more information on binary rubies.
Checking requirements for debian.
Requirements installation successful.
Installing Ruby from source to: /home/tinix/.rvm/rubies/ruby-2.5.0-preview1, this may take a while depending on your cpu(s)...
ruby-2.5.0-preview1 - #downloading ruby-2.5.0-preview1, this may take a while depending on your connection...
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100 13.4M  100 13.4M    0     0  1693k      0  0:00:08  0:00:08 --:--:-- 2192k
No checksum for downloaded archive, recording checksum in user configuration.
ruby-2.5.0-preview1 - #extracting ruby-2.5.0-preview1 to /home/tinix/.rvm/src/ruby-2.5.0-preview1....
ruby-2.5.0-preview1 - #configuring.............................................|
ruby-2.5.0-preview1 - #post-configuration..
ruby-2.5.0-preview1 - #compiling.........................................................................|
ruby-2.5.0-preview1 - #installing..............
ruby-2.5.0-preview1 - #making binaries executable..
Rubygems 2.6.14 already available in installed ruby, skipping installation, use --force to reinstall.
ruby-2.5.0-preview1 - #gemset created /home/tinix/.rvm/gems/ruby-2.5.0-preview1@global
ruby-2.5.0-preview1 - #importing gemset /home/tinix/.rvm/gemsets/global.gems.............................|
ruby-2.5.0-preview1 - #generating global wrappers........
ruby-2.5.0-preview1 - #gemset created /home/tinix/.rvm/gems/ruby-2.5.0-preview1
ruby-2.5.0-preview1 - #importing gemsetfile /home/tinix/.rvm/gemsets/default.gems evaluated to empty gem list
ruby-2.5.0-preview1 - #generating default wrappers........
ruby-2.5.0-preview1 - #adjusting #shebangs for (gem irb erb ri rdoc testrb rake).
Install of ruby-2.5.0-preview1 - #complete
Ruby was built without documentation, to build it run: rvm docs generate-ri
 tinix  
 {% endhighlight %}

 The 2.5.0-preview1Ruby language version has just been released. Because it is not a stable version, its use is not yet recommended .

** Inverse backtrace**

The **backtrace** (list of methods that were run before an error happened) will start to be displayed in reverse order. Using the following code as an example:

{% highlight ruby %}

#file test.rb

def a
   b
end

def b
   c
end

def c
   raise 'error'
end

a

{% endhighlight %}

if the same file is run in ruby 2.4 you get...

{% highlight ruby %}

$ ruby test.rb
test.rb:10:in `c': error (RuntimeError)
    from test.rb:6:in `b'
    from test.rb:2:in `a'
    from test.rb:13:in `<main>'

{% endhighlight %}

		Rescue / else / ensure will be allowed inside of / end blocks

Running with Ruby 2.4:

Currently we can only capture exceptions within methods or blocks begin/ end, ie:

{% highlight ruby %}
begin
  raise 'boom'
rescue Exception => e
  puts "Error caught: #{e.message}"
end
{% endhighlight %}

: Output Error caught: boom

{% highlight ruby %}
def my_method
  raise boom
  rescue Exception => and
  puts "Error caught: # {e.message}"
end
{% endhighlight %}

: Output Error caught: boom.

But the code below doesn't work:

{% highlight ruby %}
[1, 2, 3].map do |i|
  raise 'boom'
  rescue Exception => e
  puts "Error caught: #{e.message}"
end
{% endhighlight %}

{% highlight ruby %}
syntax error, unexpected keyword_rescue, expecting keyword_end
rescue Exception => e
{% endhighlight %}

**Running with Ruby 2.5:**

In the version that is about to be released, this is possible. The output of the above code will be:

{% highlight ruby %}
Captured error: boom
Captured error: boom
Captured error: boom
{% endhighlight %}

**New method yield_self**

According to the  [official documentation Ruby 2.5](https://docs.ruby-lang.org/en/trunk/Object.html#method-i-yield_self)

* Yields self to the block and returns the result of the block.

Although very similar to the tapclass method Object(which is very useful, by the way), your returns are different.

While with the method tapyou open a block and at the end the object itself is returned, with the yield_self, the result of the block is returned.

Example:

{% highlight ruby %}
object.tap {| obj | obj.save} # => object
{% endhighlight %}

The `save` method was called,
 but `object` is returned


{% highlight ruby %}
object.yield_self {| obj | obj.save} # => true
#The last block execution will be returned.
#That is, assuming that the `save` method returns` true`,
#the return of this entire line will be `true` too
{% endhighlight  %}

I could not think of a practical case to use it, but certainly had a reason to have been added :)

# Other changes
The new version will also bring other new features, such as support for Unicode version 10, which [includes 56 emojis created this year](https://emojipedia.org/emoji-5.0/) . You can see a complete list with all the news [in this document .](https://github.com/ruby/ruby/blob/v2_5_0_preview1/NEWS)

To install Ruby 2.5 (though not yet recommended for not being a stable release) through RVM, simply run:

```
rvm install 2.5.0-preview1
```

for more information visit [Ruby 2.5.0-preview1 Released](https://www.ruby-lang.org/en/news/2017/10/10/ruby-2-5-0-preview1-released/)

Yes!!! Enjoy Ruby 2.5.0-preview1 Released