---
layout: post
title:  "Install Ruby docs on Ubuntu 20.04"
date:   2022-08-07 22:20:11 -0700
categories: ruby
---
Ubuntu 20.04 comes with Ruby 2.7. However, it doesn't install Ruby documentations by default. As a result, developers stumble on `Nothing known about File` when they use **ri** query classes and methods in core and standard libaries. eg. 

{% highlight bash %}
$ri File
Nothing known about File
{% endhighlight %}


If we use `--list-doc-dirs` to check, we will find that ri queries system-scoped Ruby documentation from /usr/share/ri/2.7.0/system. unfortunately, it's empty by default.

{% highlight bash %}
$ ri --list-doc-dirs
/usr/share/ri/2.7.0/system
/usr/share/ri/2.7.0/site
/home/xliu/.rdoc
{% endhighlight %}

According to APT, Ubuntu 20.04(codename focal) installs package [ruby/focal](https://packages.ubuntu.com/focal/ruby). Package `ri` is one of suggests but not a hard dependency of it. [Package ri](https://packages.ubuntu.com/focal/ri) in APT is different from command `ri`, which actually comes with Ruby 2.7. One dependency of package `ri` is [ruby2.7-doc](https://packages.ubuntu.com/focal/all/ruby2.7-doc/filelis). It will populate ruby documentations to the system directory. 

By installing `ri`, APT also installs ruby2.7-doc as a dependency. After install them, Rubyists will be able to use ri to check documentations.
