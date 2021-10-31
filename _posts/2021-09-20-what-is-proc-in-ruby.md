---
title: What is Proc in Ruby
layout: post
date: '2021-09-20 20:39:07'
categories: ruby
comments: true
---

A Proc object is an encapsulation of a block of code, which can be stored in a local variable, passed to a method or another Proc, and can be called. Proc is an essential concept in Ruby and a core of its functional programming features.

{% highlight ruby %}
square = Proc.new {|x| x**2 }

square.call(3)  #=> 9
# shorthands:
square.(3)      #=> 9
square[3]       #=> 9

{% endhighlight %}

Proc objects are closures, meaning they remember and can use the entire context in which they were created.


{% highlight ruby %}
def gen_times(factor)
  Proc.new {|n| n*factor } # remembers the value of factor at the moment of creation
end

times3 = gen_times(3)
times5 = gen_times(5)

times3.call(12)               #=> 36
times5.call(5)                #=> 25
times3.call(times5.call(4))   #=> 60
{% endhighlight %}

## Creation
There are several methods to create a Proc

*  Use the Proc class constructor:

{% highlight ruby %}

proc1 = Proc.new {|x| x**2 }

{% endhighlight %}

* Use the Kernel#proc method as a shorthand of ::new:

{% highlight ruby %}

proc2 = proc {|x| x**2 }

{% endhighlight%}

* Receiving a block of code into proc argument (note the &):
* 
{% highlight ruby%}
def make_proc(&block)
  block
end

proc3 = make_proc {|x| x**2 }

{% endhighlight%}

* Construct a proc with lambda semantics using the Kernel#lambda method (see below for explanations about lambdas):

{% highlight ruby%}

lambda1 = lambda {|x| x**2 }

{% endhighlight%}

*Use the Lambda literal syntax (also constructs a proc with lambda semantics):

{% highlight ruby%}

lambda2 = ->(x) { x**2 }

{% endhighlight%}

## Lambda and non-lambda semantics
* Procs are coming in two flavors: lambda and non-lambda (regular procs). Differences are:
* In lambdas, return means exit from this lambda;

*In regular procs, return means exit from embracing method (and will throw LocalJumpError if invoked outside the method);

*In lambdas, arguments are treated in the same way as in methods: strict, with ArgumentError for mismatching argument number, and no additional argument processing;

*Regular procs accept arguments more generously: missing arguments are filled with nil, single Array arguments are deconstructed if the proc has multiple arguments, and there is no error raised on extra arguments

{% highlight ruby%}

p = proc {|x, y| "x=#{x}, y=#{y}" }
p.call(1, 2)      #=> "x=1, y=2"
p.call([1, 2])    #=> "x=1, y=2", array deconstructed
p.call(1, 2, 8)   #=> "x=1, y=2", extra argument discarded
p.call(1)         #=> "x=1, y=", nil substituted instead of error

l = lambda {|x, y| "x=#{x}, y=#{y}" }
l.call(1, 2)      #=> "x=1, y=2"
l.call([1, 2])    # ArgumentError: wrong number of arguments (given 1, expected 2)
l.call(1, 2, 8)   # ArgumentError: wrong number of arguments (given 3, expected 2)
l.call(1)         # ArgumentError: wrong number of arguments (given 1, expected 2)

def test_return
  -> { return 3 }.call      # just returns from lambda into method body
  proc { return 4 }.call    # returns from method
  return 5
end

test_return # => 4, return from proc

{% endhighlight%}

Lambdas are useful as self-sufficient functions, in particular useful as arguments to higher-order functions, behaving exactly like Ruby methods.

Procs are useful for implementing iterators:

{% highlight ruby%}
def test
  [[1, 2], [3, 4], [5, 6]].map {|a, b| return a if a + b > 10 }
                            #  ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
end

{% endhighlight%}

Inside map, the block of code is treated as a regular (non-lambda) proc, which means that the internal arrays will be deconstructed to pairs of arguments, and return will exit from the method test. That would not be possible with a stricter lambda.

You can tell a lambda from a regular proc by using the lambda? instance method.

Lambda semantics is typically preserved during the proc lifetime, including &-deconstruction to a block of code:

{% highlight ruby%}

p = proc {|x, y| x }
l = lambda {|x, y| x }
[[1, 2], [3, 4]].map(&p) #=> [1, 2]
[[1, 2], [3, 4]].map(&l) # ArgumentError: wrong number of arguments (given 1, expected 2)

{% endhighlight%}

The only exception is dynamic method definition: even if defined by passing a non-lambda proc, methods still have normal semantics of argument checking.

{% highlight ruby%}
class C
  define_method(:e, &proc {})
end
C.new.e(1,2)       #=> ArgumentError
C.new.method(:e).to_proc.lambda?   #=> true
{% endhighlight%}

This exception ensures that methods never have unusual argument passing conventions, and makes it easy to have wrappers defining methods that behave as usual.

{% highlight ruby%}
class C
  def self.def2(name, &body)
    define_method(name, &body)
  end

  def2(:f) {}
end
C.new.f(1,2)       #=> ArgumentError

{% endhighlight%}