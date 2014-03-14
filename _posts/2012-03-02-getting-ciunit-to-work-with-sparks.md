---
layout: post
title: Getting CIUnit To Work With Sparks
---

I recently got bit by the Sparks bug again. If you don't know, [Sparks](http://getsparks.org) is like CodeIgniter's version of Ruby Gems. It's a command-line-based package manager that lets you install stuff for CodeIgniter quickly and keep it up-to-date. It's a great idea and I want to port my libraries over to this system.

So I thought I'd try to get [Kenji's CIUnit](https://bitbucket.org/kenjis/my-ciunit) working with Sparks. His [wiki](https://bitbucket.org/kenjis/my-ciunit/wiki/Home) says to just change one line in ```MY_Loader.php``` (which is created by Sparks) and you're good to go. I found this to not be the case, so I did a little digging. Here's what you need to do to get them to play nice together.

<!--more-->

If you haven't already, start by [installing Sparks](http://getsparks.org/).

In ```application/core/MY_Loader.php``` change this:

{% highlight php %}
    define('SPARKPATH', 'sparks/');
{% endhighlight %}

to this:

{% highlight php %}
    define('SPARKPATH', APPPATH . '../sparks/');
{% endhighlight %}

Then in application/third_party/CIUnit/core/CIU_Loader.php change this:

{% highlight php %}
    class CIU_Loader extends CI_Loader {
{% endhighlight %}

to this:

{% highlight php %}
    class CIU_Loader extends MY_Loader {
{% endhighlight %}

Then you should be good to go. CD back to your root/tests in the terminal and hit phpunit. If you've loaded sparks, they should now work without erroring out. Huzzah!
