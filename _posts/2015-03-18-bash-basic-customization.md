---
layout: post
title:  "Bash basic customization"
date:   2015-03-18 21:13:17
category: devops
tags: [devops, bash, linux]
---

Bash is my favorite shell when it comes to servers administration. I usually configure bash with some tweaks to make my life easier, the following lines can be placed on your `~/.bash_profile` or `~/.bashrc`:

{% gist 6318d855667ff446a3b4 %}

Everything seems pretty easy, doesn't it? Well, I'll explain a little bit about the `PATH` setup:

{% highlight ruby %}
export PATH="$PATH:$HOME/bin"
{% endhighlight %}

This will add `~/bin` to your `PATH` so you can place there any script or binary file and execute/use it from anywhere.

If you want to learn more, go ahead and take a look at the [Bash Beginners Guide][bash-beginners-guide].

[bash-beginners-guide]:      http://www.tldp.org/LDP/Bash-Beginners-Guide/html/Bash-Beginners-Guide.html#sect_03_01
