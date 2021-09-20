---
title: Ruby vs Elixir ,  Rails vs Phoenix - part 2
layout: post
date: '2018-09-28 16:52:56'
categories: elixir
comments: true
---

![useful image]({{ site.url }}/images/phoenix-vs-rails.png)

Dev Tools
rake vs. mix
In Ruby, there is rake, in Elixir there is mix.


Mix is a build tool that provides tasks for creating, compiling, and testing Elixir projects, managing its dependencies, and more.

Like Rails, Phoenix provides various mix commands to handle common tasks. Most of these commands should feel familiar:

{% highlight ruby %}
mix phoenix.new my_app
mix phoenix.server
mix ecto.migrate
mix phoenix.gen.html User users email:string
mix test
MIX_ENV=test mix ecto.migrate
 {% endhighlight %}
 
 # irb vs. iex
 Ruby gives us the Interactive Ruby Shell (IRB or irb). IEx is Elixir’s Interactive Shell.

Run it within your Elixir project using the command: iex -S mix. The -S tells iex to execute the Mixfile (mix.exs), which handles configuring the project.

Unlike irb, you will have to hit Ctrl-C twice to exit, instead of Ctrl-D.

If you are like me and prefer to have a console session open while developing, usually with some state built up, then the recompile() helper will come in handy. Calling it eliminates having to start a new iex session (and lose all your state) when you've made changes to a file.

Another handy, time-saving tip:

Create a .iex.exs file in your project root to alias your project's modules so you can call, Repo.all, instead of, MyApp.Repo.all.

The first time I fired up iex and wanted to grab the first User in the database, I got hit with:

{% highlight ruby %}
(UndefinedFunctionError) function MyApp.User.first/0 is undefined or privateefinedFunctionError) function
 {% endhighlight %}
 
 Remember, Elixir is functional, so we can't do things like User.first.

Here is the equivalent in Phoenix (technically Ecto, the database layer):

{% highlight ruby %}
User |> Repo.all |> List.first
 {% endhighlight %}
 
 That is a lot of typing. Adding a couple convenience functions to my project's Repo module allows me to call Repo.first User. That is better.

{% highlight ruby %}
defmodule MyApp.Repo do
  use Ecto.Repo, otp_app: :elformo
  alias __MODULE__

  def first(query) do
    query |> Ecto.Query.first |> Repo.one
  end

  def last(query) do
    query |> Ecto.Query.last |> Repo.one
  end
end
 {% endhighlight %}
 
 <hr>