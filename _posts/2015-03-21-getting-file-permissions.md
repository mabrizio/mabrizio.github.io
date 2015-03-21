---
layout: post
title:  "Getting file pemissions"
date:   2015-03-21 12:35:37
category: devops
tags: [devops, perl, linux]
---

I have to admit it, I'm usually a little lazy so I prefer to have a bunch of scripts ready to work for me located at `~/bin`. The following Perl scripts is one of them, it has been with me for years now:

{% gist 280409a85bb31f36e3fb %}

For example, if you run it against your `$HOME` directory, you'll get something like this:

{% highlight bash %}
$ lsmod.pl $HOME
/home/username: 0755
{% endhighlight %}
