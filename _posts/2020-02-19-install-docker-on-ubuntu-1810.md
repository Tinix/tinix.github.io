---
title: Install Docker on Ubuntu 18.10
layout: post
date: '2020-02-19 00:22:50'
categories: docker
comments: true
---

![useful image]({{ site.url }}/images/instalar-docker-en-Ubuntu.jpg)
## let's install Docker
 Step 1: Update Local Database
Update the local database with the command:

{% highlight ruby %}
sudo apt-get update
{% endhighlight %}

Step 2: Download Dependencies
You’ll need to run these commands to allow your operating system to access the Docker repositories over HTTPS.

In the terminal window, type:

{% highlight ruby %}
tinix@yandex:/$ sudo apt-get install apt-transport-https ca-certificates curl software-properties-common
{% endhighlight %}

To clarify, here’s a brief breakdown of each command:

* apt-transport-https: Allows the package manager to transfer files and data over https
* ca-certificates: Allows the system (and web browser) to check security certificates
* curl: This is a tool for transferring data
* software-properties-common: Adds scripts for managing software

Step 3: Add Docker’s GPG Key
The GPG key is a security feature.

 To ensure that the software you’re installing is authentic, enter:

{% highlight ruby %}
tinix@yandex:/$ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
{% endhighlight %}

# Add the repository

{% highlight ruby %}
tinix@yandex:/$ sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
{% endhighlight %}


# Update again
{% highlight ruby %}
tinix@yandex:/$ sudo apt-get update
{% endhighlight %}

# install docker

{% highlight ruby %}
 tinix@yandex:/$ sudo apt-get install docker-ce
{% endhighlight %}

# start with the system

{% highlight ruby %}
tinix@yandex:/$ sudo systemctl enable docker
{% endhighlight %}


# add new user
for example check you user


{% highlight ruby %}
tinix@yandex:/$ whoami
tinix
$ sudo usermod -aG docker tinix
{% endhighlight %}

# leave session

{% highlight ruby %}
tinix@yandex:/$ exit
{% endhighlight %}

# start again with the new user and check

{% highlight ruby %}
tinix@yandex:/$ docker run hello-world
{% endhighlight %}



that's all folks..!!

----