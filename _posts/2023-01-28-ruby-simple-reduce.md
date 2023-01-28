---
title: Ruby Simple Reduce
layout: post
date: '2023-01-28 11:54:08'
categories: ruby
comments: true
---

I’ll show you here how to implement some functions already available for
arrays, but using reduce(), map(), and select().
uniq
This function finds a set of unique elements in an array. For example:

```
irb> [1,3,5,6,7,8,6,6,1,1].uniq
=> [1,3,5,6,7,8]
```

To implement uniq, we need a way to identify unique elements. First,
realize that a hash Hash is keyed by unique values. So, as we run reduce, we
just have to put each element as the key of a hash. If the element already
exists, the value in the hash is overwritten. So, the initial value of the memo
should be {}.

```
[1,3,5,6,7,8,6,6,1,1].reduce({}) do |memo, element|
memo[element]=element
 memo
end
```

```
⇒ {1⇒1, 3⇒3, 5⇒5, 6⇒6, 7⇒7, 8⇒8}
```

Almost. Now, we just have to pick off the keys using map:

```
[1,3,5,6,7,8,6,6,1,1].reduce({}) do |memo, element|
 memo[element]=element
  memo
end.map do |key, value|
    key
end
```


```
=> [1, 3, 5, 6, 7, 8]
```