---
title: How to Install Latest Nodejs & NPM on Debian
layout: post
date: '2018-02-01 11:48:03'
categories: npm
comments: true
---

**npm installation not working under Debian Stretch**


I just tried to install node and npm on Debian Stretch. I installed node like decribed here.

After installing nodejs-legacy too I got the node command working but npm command still won't be found.

So, I tried to install it manually via apt-get install npm but it just tells me that it can't find the package. Next I tried the "Fancy Install (Unix)" from npm repository which fails with...


{% highlight ruby  %}
install npm@latest
fetching: https://registry.npmjs.org/npm/-/npm-5.5.1.tgz
module.js:327
    throw err;
    ^

Error: Cannot find module '/tmp/npm.1272/package/bin/read-package-json.js'
    at Function.Module._resolveFilename (module.js:325:15)
    at Function.Module._load (module.js:276:25)
    at Function.Module.runMain (module.js:441:10)
    at startup (node.js:140:18)
    at node.js:1043:3
added 1 package and removed 1 package in 0.45s
/usr/bin/npm -> /usr/lib/node_modules/npm/bin/npm-cli.js
/usr/bin/npx -> /usr/lib/node_modules/npm/bin/npx-cli.js
+ npm@5.5.1
updated 1 package in 1.21s
It worked
{% endhighlight %}


later I look this a solution I things so ... and saw if install nvm and later install with nvm install npm ???
ok I go

open [https://github.com/creationix/nvm](https://github.com/creationix/nvm) 
install NVM Node Version Manager 

Install script
To install or update nvm, you can use the install script using cURL:



{% highlight ruby  %}
curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.8/install.sh | bash
{% endhighlight %}

or Wget 


{% highlight ruby  %}
wget -qO- https://raw.githubusercontent.com/creationix/nvm/v0.33.8/install.sh | bash
{% endhighlight %}


The script clones the nvm repository to ~/.nvm and adds the source line to your profile (~/.bash_profile, ~/.zshrc, ~/.profile, or ~/.bashrc).


{% highlight ruby  %}
export NVM_DIR="$HOME/.nvm"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh" # This loads nvm
{% endhighlight %}


Note: On Linux, after running the install script, if you get nvm: command not found or see no feedback from your terminal after you type:


{% highlight ruby  %}
command -v nvm
{% endhighlight %}

 or run 
{% highlight ruby  %}
nvm --version
{% endhighlight %}

later you can run ...
{% highlight ruby  %}
nvm install node
Downloading and installing node v9.5.0...
Downloading https://nodejs.org/dist/v9.5.0/node-v9.5.0-linux-x64.tar.xz...
######################################################################## 100.0%
Computing checksum with sha256sum
Checksums matched!
Now using node v9.5.0 (npm v5.6.0)
Creating default alias: default -> node (-> v9.5.0)
 tinix  ~  node -v
v9.5.0
{% endhighlight %}

look this...

{% highlight ruby  %}
 tinix  ~  node -v
v9.5.0
{% endhighlight %}


problem solved..!!!