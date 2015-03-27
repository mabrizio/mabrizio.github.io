---
layout: post
title:  "Getting file pemissions"
date:   2015-03-21 12:35:37
category: devops
tags: [devops, perl, linux]
---

I have to admit it, I'm usually a little lazy so I prefer to have a bunch of scripts ready to work for me located at `~/bin`. The following Perl scripts is one of them, it has been with me for years now:

{% highlight ruby %}
#!/usr/bin/env perl
 
use Fcntl ':mode';
 
foreach(@ARGV){
    if (($dev,$ino,$mode) = lstat($_)) {
        $permissions = sprintf "%04o", S_IMODE($mode);
        printf("$_:  $permissions\n");
    }
}
{% endhighlight %}
For example, if you run it against your `$HOME` directory, you'll get something like this:

{% highlight bash %}
$ lsmod.pl $HOME
/home/username: 0755
{% endhighlight %}
