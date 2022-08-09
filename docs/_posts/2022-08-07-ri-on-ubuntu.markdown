---
layout: post
title:  "Install Ruby docs on Ubuntu 20.04"
date:   2022-08-07 22:20:11 -0700
categories: ruby
---
Ubuntu 20.04 (codename **FocalFossa**) comes with [Ruby 2.7](https://wiki.ubuntu.com/FocalFossa/ReleaseNotes#Ruby_2.7). However, it doesn't install Ruby documentations by default. As a result, developers stumble on `Nothing known about File` when they use **ri**  to search classes and methods in core and standard libaries. eg.

{% highlight bash %}
$ ri File
Nothing known about File
{% endhighlight %}


If we use `--list-doc-dirs` to check, we will find that ri queries system-scoped Ruby documentation from /usr/share/ri/2.7.0/system. Unfortunately, it is empty on my Ubuntu.

{% highlight bash %}
$ ri --list-doc-dirs
/usr/share/ri/2.7.0/system
/usr/share/ri/2.7.0/site
/home/xliu/.rdoc
{% endhighlight %}

According to APT, Ubuntu 20.04 installs package [ruby/focal](https://packages.ubuntu.com/focal/ruby). Package `ri` is one of **suggests** but not a hard dependency of it. [Package ri](https://packages.ubuntu.com/focal/ri) in APT is different from command `ri`, which actually comes with Ruby 2.7. One dependency of package `ri` is [ruby2.7-doc](https://packages.ubuntu.com/focal/all/ruby2.7-doc/filelist). It will populate ruby documentations to the system directory.

By installing `ri`, APT also installs `ruby2.7-doc` as a dependency. After install them, Rubyists will be able to use ri to check documentations.

{% highlight bash %}
$ ri --no-pager Array.assoc
Array.assoc

(from ruby core)
----------------------------------------------------------------------
  ary.assoc(obj)   -> element_ary  or  nil

----------------------------------------------------------------------

Searches through an array whose elements are also arrays comparing
obj with the first element of each contained array using
obj.==.

Returns the first contained array that matches (that is, the first
associated array), or nil if no match is found.

See also Array#rassoc

  s1 = [ "colors", "red", "blue", "green" ]
  s2 = [ "letters", "a", "b", "c" ]
  s3 = "foo"
  a  = [ s1, s2, s3 ]
  a.assoc("letters")  #=> [ "letters", "a", "b", "c" ]
  a.assoc("foo")      #=> nil

{% endhighlight %}

Happy hacking, Rubyists!
