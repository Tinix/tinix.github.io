---
layout: post
title: Build ports from package rpm or deb
dat: 2016-03-19 12:07:27 -0300
categories: FreeBSD, jekyll , programming, yandex browser
comments: true
---

This is situation : my original bad idea is a build package Yandex Browser , actualy running for mac , windows and Linux but not for FreeBSD, these were some response of this whole project... 

Tinix asked  :
Someone built a ports from a rpm or deb package? I have not the slightest idea, but surely someone could guide me...
I have a project, something not finished running FreeBSD is a benefit for the whole community
thank you very much.
Tinix.


Reply:
An RPM or DEB is similar to our pkg(8). That is to say, somebody took the original, upstream, source and built an RPM or DEB binary package from it. Instead of trying to crowbar a RedHat or Debian Linux pre-compiled binary package into FreeBSD you should take the original source and create a FreeBSD pre-compiled binary pkg(8).

other Reply:
What do you mean saying "someone built a ports from a rpm or deb package"? New ports are created taking original source and then patching them to work on FreeBSD.
If you want to port a new program to FreeBSD you should start from sources, not from already compiled binaries.
Instead, if you want to install rpm or deb packages, there are both archive/rpm4 and archive/dpkg in ports. However I don't see the point of using them, if not with linux compatibility.
EDIT: SirDice sorry, I posted before seeing your reply :oops:
 
and other reply:
That's how the Linux ports are built on FreeBSD. They take a .rpm or .deb (binary distribution, not source) of the software in question and extract that file to the work directory of the port and then after fixing what has to be fixed a pkg package is created from the extracted files. Take a look at for example emulators/linux_base-c6 for how it's done.

Tinix reply:
I'm sorry I explain wrong, now I understand,
I get the original source code
should ask the company and then compile
the company currently has packages running for mac, windows and linux, but not for FreeBSD
