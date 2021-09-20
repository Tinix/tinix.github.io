---
title: Before_validation and  after_touch callbacks in Rails
layout: post
date: '2017-09-26 09:00:40'
categories: ruby , rails
comments: true
---

Rails provide us with some pre-defined methods or hooks which can be invoked after or before the execution of a certain method in the object life cycle.
Callbacks are called in certain moments of object's life cycle which we will get to know in this blog.
Today we will be studying about three callbacks as follows :
before_validation
As the name suggests, this method is called before validation of all the fields of the form.
For example, there is a registration form which has an email field, so as soon as the user will fill the email field and submit the form before the value gets saved into the database we have to make sure that all characters in the email should be down case.
So in this case, we will invoke a before_validation callback in which we will define a method to be called before the create method is called.
In this method, we will convert the whole string into down case and after that, the create method will be called like this.

```
class Employee < ApplicationRecord
  
  before_validation :normalize_email, on: :create
 
  # :on takes an array as well
  
  def create
    ...
  end 
  protected
    def normalize_email
      self.email = email.downcase.titleize
    end
end
```

after_touch
Whenever an object is being touched the after_touch callback is called .
For example
We create an employee object and as soon as we touch the object the after_touch callback is invoked.


```
class Employee < ApplicationRecord
  
  after_touch do |employee|
    puts "The object has been touched"
  end
end
 
>> e = Employee.create(name: 'Tom')
=> #<Employee id: 1, name: "Tom", created_at: "2013-11-25 12:17:49", updated_at: "2013-11-25 12:17:49">
 
>> e.touch
The object has been touched
=> true
```

So hope this article was helpful to understand both the callbacks.