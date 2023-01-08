---
title: Rust “Hello World!” in three languages
layout: post
date: '2023-01-08 21:26:51'
categories: rust
comments: true
---

For our first program, we want to write something that outputs the following text in
multiple languages:
Hello, world!
Grüß Gott!
ハロー・ワールド
You have probably seen the first line. The other two are there to highlight a few of Rust’s features: easy iteration and built-in support for Unicode.

{% highlight ruby %}
fn greet_world() { 
  println!("Hello World");
  let southern_germany = "Grüß Gott!";
  let japan = "ハロー・ワールド";
  let regions = [southern_germany, japan];
  for region in regions.iter() { 
    println!("{}", &region);
  }
}

fn main() { 
  greet_world();
}

{% endhighlight %}

Now that src/main.rs is updated, execute cargo run from the hello2/ directory. You
should see three greetings appear after some output generated from cargo itself:

{% highlight ruby %}
$ cargo run
Finished dev [unoptimized + debuginfo] target(s) in 0.95s
Running `target/debug/hello-world`
Hello, world!
Grüß Gott!
ハロー・ワールド

{% endhighlight %}

Let’s take a few moments to touch on some of the interesting elements of Rust from
One of the first things that you are likely to notice is that strings in Rust are able to include a wide range of characters. Strings are guaranteed to be encoded as UTF-8.
This means that you can use non-English languages with relative ease.
The one character that might look out of place is the exclamation mark after
println. If you have programmed in Ruby, you may be used to thinking that it is used
to signal a destructive operation. In Rust, it signals the use of a macro. Macros can be
thought of as fancy functions for now. These offer the ability to avoid boilerplate code.
In the case of println!, there is a lot of type detection going on under the hood so
that arbitrary data types can be printed to the screen.