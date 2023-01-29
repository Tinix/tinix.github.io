---
title: Ruby Simple Reduce
layout: post
date: '2023-01-28 11:54:08'
categories: ruby
comments: true
---

I’ll show you here how to implement some functions already available for
arrays, but using reduce(), map(), and select().

## uniq
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
memo[element] = element
  memo
end.map do |key, value|
    key
end
```


```
=> [1, 3, 5, 6, 7, 8]
```

## reverse
This function reverses the order of the elements in an array:

```
irb> [1,3,5,6,7,8,6,0].reverse
```

```
=> [0, 6, 8, 7, 6, 5, 3, 1]
```

One way to solve this is to keep pushing each element on a stack.
A stack is just an array where you use unshift to push an element onto
the front, and shift to pop elements off the front. The initial value of the
reduce memo is a blank array. I put a print statement so you can see for
yourself how the memo builds up.

```
[1,3,5,6,7,8,6,0].reduce([]) do |memo, element|
memo.unshift element
  puts "After unshifting element: #{element}, the memo is:
#{memo.inspect}"
  memo
end
```

The output is as follows:

```
After unshifting element: 1, the memo is: [1]
After unshifting element: 3, the memo is: [3, 1]
After unshifting element: 5, the memo is: [5, 3, 1]
After unshifting element: 6, the memo is: [6, 5, 3, 1]
After unshifting element: 7, the memo is: [7, 6, 5, 3, 1]
After unshifting element: 8, the memo is: [8, 7, 6, 5, 3, 1]
After unshifting element: 6, the memo is: [6, 8, 7, 6, 5, 3, 1]
After unshifting element: 0, the memo is: [0, 6, 8, 7, 6, 5, 3, 1]
=> [0, 6, 8, 7, 6, 5, 3, 1]
```

## max
This function finds the largest element in an array:

```
irb> [1,3,5,6,7,8,6,0].max
```

```
=> 8
```

Reduce will work here because as you iterate through the array, you
save the largest value in the memo. This example does not even need an
explicit initial value, because the first element is the default value for the
memo.

```
[4,3,5,6,7,8,6,0].reduce do |memo, element|
if element > memo
   memo = element
 else
   memo = memo
end
puts "The largest element after checking #{element} is #{memo}"
memo
end
```

```
The largest element after checking 3 is 4
The largest element after checking 5 is 5
The largest element after checking 6 is 6
The largest element after checking 7 is 7
The largest element after checking 8 is 8
The largest element after checking 6 is 8
The largest element after checking 0 is 8
=> 8
```

Of course, the terse way to encode this is as follows:

```
[4,3,5,6,7,8,6,0].reduce do |memo, element|
 (element > memo) ? element : memo
end
=> 8
```