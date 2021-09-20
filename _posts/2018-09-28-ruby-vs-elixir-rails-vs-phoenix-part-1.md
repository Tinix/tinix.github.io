---
title: Ruby vs Elixir ,  Rails vs Phoenix - part 1
layout: post
date: '2018-09-28 16:52:56'
categories: elixir
comments: true
---

![useful image]({{ site.url }}/images/ruby-elixir.png)


This is not a, "Which is better?", post. It is more a way to help other developers, like myself, who have a background in Rails development and are interested in Elixir and Phoenix.

Elixir != Ruby and Phoenix != Rails. Even though there may be some similarities between both, it is beneficial to stay open to innovative and often lateral approaches in Elixir/Phoenix.

If you are a Ruby/Rails developer who is interested in adding Elixir/Phoenix to your toolbelt, then I hope this post serves as a helpful starting point.

{% highlight ruby %}
class User < Struct.new(:first, :last)
  def self.full_name(user)
    "#{user.first} #{user.last}"
  end
end

user = User.new("George", "Tinix")
User.full_name(user) 
#=> "George Tinix"
 {% endhighlight %}
 
 Notice that we pass user to the full_name method. There are no "object instances" to call methods on in Elixir.
 
 {% highlight ruby %}
defmodule User do
  defstruct [:first, :last]

  def full_name(user) do
    "#{user.first} #{user.last}"
  end
end

user = %User{first: "George", last: "Tinix"}
User.full_name(user)
#=> "George Tinix"
 {% endhighlight %}
	
# Embrace Pattern Matching
In Ruby, conditionals are predominant, but in Elixir it is more favorable to use pattern matching.

In Ruby, you might see something like this:

{% highlight ruby %}
def notify_user(user)
  if user.send_emails? do
   #Send emails
  end
end
 {% endhighlight %}
 
 In Elixir, we would use pattern matching against the data structure of the user argument:
 
 {% highlight ruby %}
 def notify_user(%User{send_emails?: true}) do
  #Send emails
end
def notify_user(user), do: user
 {% endhighlight %}
 The above example shows the use of pattern matching within function definitions but we can also use pattern matching to control the flow of logic.

In Rails, this could be considered the equivalent of returning a Result object for handling outcomes beyond just true or false.

In Elixir, you would utilize pattern matching on a function's result. The following is quite common to see in Phoenix controllers:
 
 {% highlight ruby %}
 case MyApp.do_something() do
  {:ok, value}     -> # do stuff ...
  {:error, errors} -> # do different stuff...
end
 {% endhighlight %}
 
 <hr>