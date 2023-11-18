---
title: 'Rust  three fundamental concepts: ownership, borrowing, and lifetimes.'
layout: post
date: '2023-11-18 19:30:00'
categories: rust
comments: true
---

In Rust, the ownership system is a key feature that enables memory safety without the need for a garbage collector. This system is based on three fundamental concepts: ownership, borrowing, and lifetimes.

Let's take a look at a simple example to illustrate how Rust manages memory without garbage collection:


{% highlight ruby %}
fn main() {
    let mut str = String::from("Hello Rust!");

    str.push_str(" How are you?");
    println!("{}", str);

    let str2 = takes_and_gives_back(str);

    println!("{}", str2);
}


fn takes_and_gives_back(some_string: String) -> String {
    let result = some_string + " Have a great day!";

    result
}
{% endhighlight %}


In this example:

We create a String and manipulate it.
The ownership of the String is transferred to the takes_and_gives_back function.
Inside the function, we perform operations on the String, and then the ownership is transferred back to the calling function.
The original String is now owned by the variable str2.
Rust's ownership system ensures that there is always one and only one owner for a piece of data. This guarantees memory safety without the need for garbage collection because the ownership system allows Rust to statically analyze the code and ensure that references to data are always valid. If you try to use a variable after it has been moved or deallocated, the Rust compiler will catch it at compile time, preventing common memory-related bugs.