---
title: Elixir  - Maps
layout: post
date: '2021-11-10 18:16:18'
categories: elixir
comments: true
---

## Maps
Whenever you need a key-value store, maps are the “go to” data structure in Elixir. A map is created using the ```%{}``` syntax:

{% highlight ruby %}

iex> map = %{:a => 1, 2 => :b}
%{2 => :b, :a => 1}
iex> map[:a]
1
iex> map[2]
:b
iex> map[:c]
nil

{% endhighlight %}

Compared to keyword lists, we can already see two differences:

 * Maps allow any value as a key.
 * Maps’ keys do not follow any ordering.

In contrast to keyword lists, maps are very useful with pattern matching. When a map is used in a pattern, it will always match on a subset of the given value:


{% highlight ruby %}

iex> %{} = %{:a => 1, 2 => :b}
%{2 => :b, :a => 1}
iex> %{:a => a} = %{:a => 1, 2 => :b}
%{2 => :b, :a => 1}
iex> a
1
iex> %{:c => c} = %{:a => 1, 2 => :b}
** (MatchError) no match of right hand side value: %{2 => :b, :a => 1}

{% endhighlight %}

As shown above, a map matches as long as the keys in the pattern exist in the given map. Therefore, an empty map matches all maps.

Variables can be used when accessing, matching and adding map keys:


{% highlight ruby %}

iex> n = 1
1
iex> map = %{n => :one}
%{1 => :one}
iex> map[n]
:one
iex> %{^n => :one} = %{1 => :one, 2 => :two, 3 => :three}
%{1 => :one, 2 => :two, 3 => :three}

{% endhighlight %}

[The Map module](https://hexdocs.pm/elixir/Map.html) provides a very similar API to the ```Keyword``` module with convenience functions to manipulate maps:

{% highlight ruby %}
iex> Map.get(%{:a => 1, 2 => :b}, :a)
1
iex> Map.put(%{:a => 1, 2 => :b}, :c, 3)
%{2 => :b, :a => 1, :c => 3}
iex> Map.to_list(%{:a => 1, 2 => :b})
[{2, :b}, {:a, 1}]
{% endhighlight %}

Maps have the following syntax for updating a key’s value:

{% highlight ruby %}
iex> map = %{:a => 1, 2 => :b}
%{2 => :b, :a => 1}

iex> %{map | 2 => "two"}
%{2 => "two", :a => 1}
iex> %{map | :c => 3}
** (KeyError) key :c not found in: %{2 => :b, :a => 1}
{% endhighlight %}

The syntax above requires the given key to exist. It cannot be used to add new keys. For example, using it with the ```:c``` key failed because there is no ```:c ``` in the map.

When all the keys in a map are atoms, you can use the keyword syntax for convenience:

{% highlight ruby %}
iex> map = %{a: 1, b: 2}
%{a: 1, b: 2}
{% endhighlight %}

Another interesting property of maps is that they provide their own syntax for accessing atom keys:

{% highlight ruby %}
iex> map = %{:a => 1, 2 => :b}
%{2 => :b, :a => 1}

iex> map.a
1
iex> map.c
** (KeyError) key :c not found in: %{2 => :b, :a => 1}
{% endhighlight %}

Elixir developers typically prefer to use the ```map.field``` syntax and pattern matching instead of the functions in the ```Map```  module when working with maps because they lead to an assertive style of programming. [This blog post by José Valim](https://dashbit.co/blog/writing-assertive-code-with-elixir) provides insight and examples on how you get more concise and faster software by writing assertive code in Elixir.

### Nested data structures

Often we will have maps inside maps, or even keywords lists inside maps, and so forth. Elixir provides conveniences for manipulating nested data structures via the ```put_in/2``` , ```update_in/2```  and other macros giving the same conveniences you would find in imperative languages while keeping the immutable properties of the language.

Imagine you have the following structure:

{% highlight ruby %}
iex> users = [
  john: %{name: "John", age: 27, languages: ["Erlang", "Ruby", "Elixir"]},
  mary: %{name: "Mary", age: 29, languages: ["Elixir", "F#", "Clojure"]}
]
[
  john: %{age: 27, languages: ["Erlang", "Ruby", "Elixir"], name: "John"},
  mary: %{age: 29, languages: ["Elixir", "F#", "Clojure"], name: "Mary"}
]
{% endhighlight %}

We have a keyword list of users where each value is a map containing the name, age and a list of programming languages each user likes. If we wanted to access the age for john, we could write:

{% highlight ruby %}
iex> users[:john].age
27
{% endhighlight %}

It happens we can also use this same syntax for updating the value:

{% highlight ruby %}
iex> users = put_in users[:john].age, 31
[
  john: %{age: 31, languages: ["Erlang", "Ruby", "Elixir"], name: "John"},
  mary: %{age: 29, languages: ["Elixir", "F#", "Clojure"], name: "Mary"}
]
{% endhighlight %}

The ```update_in/2```  macro is similar but allows us to pass a function that controls how the value changes. For example, let’s remove “Clojure” from Mary’s list of languages:

{% highlight ruby %}
iex> users = update_in users[:mary].languages, fn languages -> List.delete(languages, "Clojure") end
[
  john: %{age: 31, languages: ["Erlang", "Ruby", "Elixir"], name: "John"},
  mary: %{age: 29, languages: ["Elixir", "F#"], name: "Mary"}
]
{% endhighlight %}


There is more to learn about ```put_in/2```  and ```update_in/2```, including the ```get_and_update_in/2```  that allows us to extract a value and update the data structure at once. There are also ```put_in/3```,  ```update_in/3```  and ```get_and_update_in/3```  which allow dynamic access into the data structure. 

This concludes our introduction to associative data structures in Elixir. You will find out that, given keyword lists and maps, you will always have the right tool to tackle problems that require associative data structures in Elixir.