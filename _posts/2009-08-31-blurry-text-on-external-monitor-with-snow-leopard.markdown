---
layout: post
title: Blurry Text on External Monitor with Snow Leopard
categories:
- Posts
tags:
- apple
- blurry
- font
- mac
- smoothing
- Snow Leopard
- text
comments: true
meta:
  dsq_thread_id: '110 http://blog.petersendidit.com/?p=110'
---
One of the problems I have off and on with my MacBook Pro is that every once and a while when I have it plugged in to my Dell 2408WFP monitor the text in Terminal and [Coda](http://www.panic.com/coda/) seem to have blurry text.  Its like the font smoothing that Mac has built in has been turned of just for those applications.  When I installed Snow Leopard this problem was on all the time, nothing I tried seemed to get rid of it.

Looks like I wasn't the only one with this problem because the great guys over at [Mac OS X Hints](http://www.macosxhints.com/) just posted [a hint](http://www.macosxhints.com/article.php?story=20090828224632809) that will fix this problem.  Sounds like there is a bug in Snow Leopard that turns off the font smoothing for some external monitors.  Of course none of the Apple monitors have this problem but if you didn't shell out the extra cash for one of their beautiful monitors you might have this problem.  The fix is very simple,  just open up Terminal and then paste in:

```bash
defaults -currentHost write -globalDomain AppleFontSmoothing -int 2
```

You can try out using 1 or 3 as the value you are setting to have less or more font smoothing. You will need to restart the app you are having problems with and may even need to unplug and replug in your monitor.

if you decide you just want to get rid of the change just open up terminal and paste in:

```bash
defaults -currentHost delete -globalDomain AppleFontSmoothing
```

This will remove the key/value pair that you added and you will be back to the default Snow Leopard way of font smoothing.

[MacOSXHints - Re-enable LCD font smoothing for some monitors](http://www.macosxhints.com/article.php?story=20090828224632809)

EDIT (9/11/2009)
Looks like you can also set the value back to the default value by going in to System Preferences and selecting the "Automatic Font Smoothing" checkbox, this is found at the bottom of the "Appearance" section.
