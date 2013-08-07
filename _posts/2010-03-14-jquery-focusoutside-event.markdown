---
layout: post
title: jQuery focusoutside event
categories:
- Posts
tags:
- clickoutside
- focusin
- focusoutside
- jQuery
- Stackoverflow
comments: true
meta:
  dsq_thread_id: '153 http://blog.petersendidit.com/?p=153'
---
I was doing my part helping out on [StackOverflow](http://stackoverflow.com/) in the jQuery tag yesterday and ran across a [question asking how to hide a div on blur of an input field as long as the click wasn't inside a div that "connected" to that input field](http://stackoverflow.com/questions/2426438/2427363).  What I ended up with for an [answer](http://stackoverflow.com/questions/2426438/2427363#2427363) was to bind a click and a focusin event on the document and check of the event.target was or is a child of the div we care about.  The [focusin event](http://api.jquery.com/focusin/) is a special focus event the bubbles since the normal focus event does not. I needed to use the focusin event incase the user tabbed to the next field rather then clicking. This got me thinking, [Ben Alman](http://benalman.com/) created a custom [jQuery event 'clickoutside'](http://benalman.com/projects/jquery-clickoutside-plugin/) for those times when you need to know that the user just clicked outside of your div and you should now close it. If the same code could also handle the focusin event then it would make answering that question very slick.  So I [forked](http://github.com/petersendidit/jquery-clickoutside/blob/master/jquery.ba-clickoutside.js) Ben Alman's clickoutside event on github and did some [hacking to add the focusoutside event](http://github.com/petersendidit/jquery-clickoutside/blob/master/jquery.ba-clickoutside.js).  I am sure the code could be shorted up even more then it is now but it works nicely.

**UPDATE**

My hacking inspired Ben to do some hacking of his own and we worked on making the plugin work for all the native jQuery events that made since to have outside versions.  Check out the new [jQuery Outside Events](http://benalman.com/projects/jquery-outside-events-plugin/).