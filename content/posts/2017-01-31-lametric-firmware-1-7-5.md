---
title: LaMetric Firmware 1.7.5
author: Alex
type: posts
date: 2017-01-31T22:37:29+00:00
url: /posts/lametric-firmware-1-7-5/
categories:
  - Article
tags:
  - Home Assistant
  - LaMetric
  - Python

---
A new firmware for the LaMetric Time is out &#8211; [version 1.7.5][1] has some nice things to offer for those of us who would like to use the device in home automation (sadly the documentation is not yet updated). While this has been announced in the change log for 1.7.4, there have been some bugs and there are still one or two things that needs fixing, but that&#8217;s just minor stuff.

So, lets dive right in: You can control the LaMetric time nearly completely via the REST-API. You can

  * switch between apps (previous or next, just like hitting the buttons on the device)
  * switch directly to a specific app
  * control the radio (on, off, switch channel &#8211; but not add or edit channels)
  * set alarms and enable or disable them
  * start/stop/reset the stopwatch
  * start/stop/reset/set the countdown

This is all on top off the already existing features (accessing device information about WiFi, Bluetooth, volume, display etc.)

This means nearly everything that had to be done using the iOS/Android app before, can now be done using any programming language you want.

I explained in my [previous][2] [articles][3] how to sent notifications &#8211; and it&#8217;s basically the same with the new controls. I&#8217;ve used PHP in the articles, because it&#8217;s what most people in the forum requested, but personally I use Python.

Until now I had written some scripts, without a specific library,  just a bunch of requests in a file which did the things I wanted. But when I discovered the new features I chose to clean my code and maybe make a Python package out of it &#8211;  at least a simple class for interacting with the device.

As any programmer should do, I did a search on GitHub to see if there are already some libraries. And of course I found one &#8211; [lmnotify][4] was relatively up to date and [so I forked it][5] and added some new code. Today I sent my pull request and it was already merged. This package is also available via PIP and it  supports all the features that I mentioned above.

Feel free to use this package, sent bugs, feature requests, pull requests.

&nbsp;

Next I&#8217;ll be working on adding support for the LaMetric Time to [Home Assistant][6] &#8211; a platform for home automation that I&#8217;ve been using for a while and I think I already saw something LaMetric related, but without the features from the new firmware it&#8217;s useless for me.

 [1]: http://firmware.lametric.com
 [2]: https://blog.aruehe.io/lametric-local-push/
 [3]: https://blog.aruehe.io/lametric-firmware-1-6-0-and-local-push/
 [4]: https://github.com/keans/lmnotify
 [5]: https://github.com/alexrockt/lmnotify
 [6]: https://home-assistant.io