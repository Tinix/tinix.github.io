---
title: Flash Messages in Rails
layout: post
date: '2020-02-25 00:35:08'
categories: ruby
comments: true
---

# What are flash messages?

A flash message is a way to communicate information with the users of your Rails application so they can know what happens as a result of their actions.

Example messages:

“Password changed correctly” (confirmation)
“User not found” (error)
You set these flash messages in your controllers, then you render them in your views. Your users can then act accordingly.

Let’s learn exactly how this works!

#  **How to Use Flash Messages**

You can work with these notification messages using the flash helper method.

It behaves a lot like a Ruby hash.

The flash object has methods like keys, any? or each & you can access a particular message with [].

What types of flash messages can you set?

By default you have:

1. notice
2. alert


Here’s an example of how to use it:

{% highlight ruby %}
flash.alert = "User not found." 
{% endhighlight %}

## Or if you prefer:

{% highlight ruby %}
flash[:alert] = "User not found." 
{% endhighlight %}

(Only a style difference.)

You can use this code inside your controller actions, like index, create, new, etc.

Another way is this:

{% highlight ruby %}
redirect_to :books_path, notice: "Book not found"
{% endhighlight %}
 

This allows you to redirect & create a flash message in one step.

Nice!

# Alert vs Notice
As far as I understand it doesn’t really matter if you use alert or notice.

Use the one that feels more natural for your situation.

I like to think about alert as an error message & a notice as a confirmation message.

Separating them helps you style them differently.

# For example:

You can show alerts in red & notices in green.

It’s also possible to create your own flash types by using the add_flash_types controller method.

# Like this:

{% highlight ruby %}
class ApplicationController
  add_flash_types :info, :error, :warning
end 
{% endhighlight %}


# Rendering Flash Messages

Flash messages aren’t shown automatically.

You have to render them inside one of your views so users can see them.

Consider adding this to your application layout.

## Here’s a code example:

{% highlight ruby %}
<% flash.each do |type, msg| %>
  <div>
    <%= msg %>
  </div>
<% end %>
{% endhighlight %}


Put this wherever you want to show your notice, usually at the top of the page, below the menu bar.

Remember:

Once you render a message it’ll be removed from flash, so it won’t be shown again.

Styling Your Notices & Alert Messages

Flash messages don’t have any built-in design or style.

Solution?

If you’re using Bootstrap, you can use the "alert alert-info" CSS class to make flash messages look good.

Example:

{% highlight ruby %}
<% flash.each do |type, msg| %>
  <div class="alert alert-info">
    <%= msg %>
  </div>
<% end %>
{% endhighlight %}

It looks like this:

If you’re NOT using Bootstrap, then you can write your own CSS to make it look however you want.

# When Are Flash Messages Rendered?


Flash messages are only removed on your next controller action, after your display them.

Implications:

If you redirect_to, then render a flash message, that’s good
If you redirect_to & DON’T render the message, the message will stick around, in the flash hash
If you render on the same action that you’re setting the flash message, that flash message will be available, but NOT removed so it will stay around & potentially be shown twice
So…

What if you want to set a flash message for the current action?

That’s where flash.now comes in!

Here’s an example:

{% highlight ruby %}
def index
  @books = Book.all

  flash.now[:notice] = "We have exactly #{@books.size} books available."
end
{% endhighlight %}


This will render the index view.

The notice message will be shown & removed from flash so it won’t be shown twice.

In other words:

You only need to use flash.now if you’re going to render instead of redirecting.

# Summary
You’ve learned about flash messages in Rails & how to use them correctly!

Btw, flash messages aren’t the same as validation errors. Validations are associated with the model object, and you access these validation messages with the errors method, like @user.errors.

Now it’s your turn to put this into practice by writing some code.

Thanks for reading!
	
---