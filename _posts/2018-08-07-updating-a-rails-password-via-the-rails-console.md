---
title: Updating a rails password via the rails console
layout: post
date: '2018-08-07 16:47:20'
categories: ruby
comments: true
---

I forgot one of my test passwords and realized I didn’t have a quick way to redo the password. There is a simple handful of commands fix this:


{% highlight ruby  %}

irb(main):001:0> u = User.find_by_id(1)
  User Load (3.5ms)  SELECT "users".* FROM "users" WHERE "users"."id" = 1 LIMIT 1
=> #<User id: 1, name: "JJ Asghar", email: "jjasghar@gmail.com", created_at: "2014-04-18 17:46:48", updated_at: "2014-04-25 23:21:10", password_digest: "$2a$10$or/wJw1I8Wpf0lXNbtawveoQXETGJbUkv/VwXQXzn92r...", remember_token: "uUJTExCyt4mpAOpQWd4PMA">
irb(main):002:0> u
=> #<User id: 1, name: "JJ Asghar", email: "jjasghar@gmail.com", created_at: "2014-04-18 17:46:48", updated_at: "2014-04-25 23:21:10", password_digest: "$2a$10$or/wJw1I8Wpf0lXNbtawveoQXETGJbUkv/VwXQXzn92r...", remember_token: "uUJTExCyt4mpAOpQWd4PMA">
irb(main):003:0> u.password = "a_stupid_pa$$word"
=> "_stupid_pa$$word"
irb(main):004:0> u.password_confirmation = "a_stupid_pa$$word"
=> "_stupid_pa$$word"
irb(main):005:0> u.save
   (2.0ms)  BEGIN
  User Exists (12.2ms)  SELECT 1 AS one FROM "users" WHERE (LOWER("users"."email") = LOWER('jjasghar@gmail.com') AND "users"."id" != 1) LIMIT 1
   (15.8ms)  UPDATE "users" SET "password_digest" = '$2a$10$Za7prnrSthhE90AvB15BNOMl8sf3oL7onBpZ45nH/9skwHfn1EFA.', "remember_token" = 'zOZYjEVovO143qrX1yhibw', "updated_at" = '2014-04-25 23:24:39.329502' WHERE "users"."id" = 1
   (4.6ms)  COMMIT
=> true
irb(main):006:0>

{% endhighlight %}


As you can see, you need to create an object via a find_by_<something>, in my case id and write it to u. After that I change the password key to a_stupid_pa$$word along with the password_confirmation. I then write it to the database via u.save.