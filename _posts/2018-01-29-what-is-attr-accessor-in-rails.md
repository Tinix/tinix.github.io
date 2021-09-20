---
title: What is attr_accessor in Rails?
layout: post
date: '2018-01-29 20:15:02'
categories: ruby
comments: true
---

attr_accessor is used to **define an attribute for object of Model which is not mapped with any column in database**. This answers question - What is attr_accessor in Rails.

**1. attr_accessor Methods**

attr_accessor creates two methods i.e. getter method and setter method.

**getter method **- it is used to retrieve value of the attribute

**setter method** - it is used to set value to the attribute

**When to use attr_accessor in Rails?**

Whenever you want to show certain attribute for particular form but you do not want to store it’s value in the database then you use attr_accessor for that model as follows,

Suppose we have a Model called user in out database with following fields,


* id
* name
* age
* city
* profession

And we define attr_accessor :type_of_user as follows,

{% highlight ruby  %}
Class User < ActiveRecord::Base
   attr_accessor :type_of_user
end
{% endhighlight %}

Now, whenever you create a object of the class User then you can assign a value to it’s attr_accessor.

{% highlight ruby  %}
new_user = User.new(:name => 'Albert', :age => 23, :city => 'Ports S.')
{% endhighlight %}

This will create new object of class User and assign given attribute values. You can assign value to attr_accessor variable as follows,


{% highlight ruby  %}
ew_user.type_of_user = 'middle-aged'
{% endhighlight %}

This assigns ‘middle-aged’ value to the attribute type_of_user attr_accessor.

getter and setter in Action
For attribute type_of_user getter and setter methods are created as follows,


{% highlight ruby  %}
# getter
def type_of_user
  @type_of_user
end

# setter
def type_of_user=(val)
  @type_of_user = val
end
{% endhighlight %}


And these are used whenever we assign or retrieve values from the attr_accessor.


2. Usage in Classes
Whenever changing value of the attr_accessor variables, we need to use self.variable_name =  to assign new value to the variable. Otherwise, it will consider it as a local variable resulting into incorrect values.

For example,

{% highlight ruby  %}
class SimpleService

  attr_accessor :name

  def initialize(name)
    @name = name
  end

  def process
    if false # some condition met
      name = 'Akshay'
    end
    name
  end
end
{% endhighlight %}

Here, it the above service class we have defined name as the attr_accessor. We need to change it’s value based on some condition. And we return it’s value from process method.

When we execute this class as,

{% highlight ruby  %}
SimpleService.new('John Doe').process
=> nil
{% endhighlight %}


We can see that process method has returned nil.

Explaination

In the block,

{% highlight ruby  %}
def process
  if false # some condition met
    name = 'Akshay'
  end
  name
end
{% endhighlight %}

As the if condition is false, and value of name is returned from the process method, name is considered as the local variable. Local variable name does not have any value. Thus, it returns nil.

Correction

To correct the above service class, we need to use explicity self when assigning value to the attr_accessor variable as given below,

{% highlight ruby  %}
class SimpleService

  attr_accessor :name

  def initialize(name)
    @name = name
  end

  def process
    if false # some condition met
      self.name = 'Akshay'
    end
    name
  end
end
{% endhighlight %}


Now if we execute this class, we will get expected result as given below.


{% highlight ruby  %}
SimpleService.new('John Doe').process
=> "John Doe"
{% endhighlight %}

3. Lifetime of attr_accessor
attr_accessor is accessible throughout object’s lifecycle. When object is saved using any of ActiveRecord method, save, update etc. all attributes of Model other than attr_accessor are saved in the database.

How to Access
Throughout lifecycle of object, you can access the value of attribute accessor as follows,

{% highlight ruby  %}
new_user.type_of_user
{% endhighlight %}

3. Conclusion
We learned what is attr_accessor in Rails and how to use it with Rails .




