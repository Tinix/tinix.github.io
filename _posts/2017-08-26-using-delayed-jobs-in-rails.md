---
title: Using Delayed Jobs in Rails
layout: post
date: '2017-09-26 09:00:40'
categories: ruby
comments: true
---

When creating a web application sometimes need arises that we have to schedule some jobs during the execution of a particular method. Due to these job the render of the page has to wait until the task gets over.
This waiting can be sometimes annoying because a user who is waiting for a job to get completed will have to wait for a lot of time if the number of jobs to be performed is more.
For example if we take the scenario of sending mails to the user. Now for this if we have large number of users to whom we want to send a mail from our application so it will take a lot of time to get completed which no one will like to wait. 
So by using delayed jobs what we can do is we can execute the processes in the background and user wont have to wait till all the processes are completed. 
For that we will be using a gem called 

{% highlight ruby %}
gem 'delayed_job_active_record'
{% endhighlight %}

place this gem in your gemfile and run bundle install.
Now after done with this we need to add the generator of this gem because active record actice records backend requires a job table in which the jobs will be stored in a queue. You can create the table by running the following command

{% highlight ruby %}
rails generate delayed_job:active_record
{% endhighlight %}

and then run rake db:migrate
Now when using this in development mode we need to set the queue_adapter in config/application.rb

{% highlight ruby %}
config.active_job.queue_adapter = :delayed_job
{% endhighlight %}

with the help of this queue adapter we dont need to restart delayed Job every time we update our code in development.
Now once done with this we will have to start the rake job in our console which will allow the jobs to run in the background without having the need to restart it again and again. We need to write this in console

{% highlight ruby %}
rake jobs:work
{% endhighlight %}

This will start the rake job thread and will wait for a process or a task to come to it.
Now last thing which we need to do is call the delay method where we actually need our jobs to be processed in background without affecting the current execution. 
Suppose oif you are sending a mail to all the users who have subscribed for a magazine so the users wont have to wait until the mail is sent to all the users. we will just add the delay method like this

{% highlight ruby %}
NotificationMailer.delay.notification_email(email)
{% endhighlight %}

Here notification mailer is the name of the mailer and notification_email is the method through which the mail is being sent. Now the mail will be sent to all users in the background and the execution of the method wont be delayed.