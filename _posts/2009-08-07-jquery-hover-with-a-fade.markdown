---
layout: post
title: jQuery hover with a fade
categories:
- Posts
tags:
- animate
- fadeIn
- fadeOut
- hover
- jQuery
comments: true
meta:
  dsq_thread_id: '69 http://blog.petersendidit.com/?p=69'
---
[@rmurphey](http://twitter.com/rmurphey) sent out a question on twitter yesterday that I got interested in.

<blockquote class="twitter-tweet"><p><a href="https://twitter.com/search?q=%23jquery&amp;src=hash">#jquery</a> on hover, i want to stop a fade, clear the anim queue, and start an opposite fade -- what am i doing wrong? http://bit.ly/QykYd</p>&mdash; Rebecca Murphey (@rmurphey) <a href="https://twitter.com/rmurphey/statuses/3172843041">August 7, 2009</a></blockquote>
<script async src="//platform.twitter.com/widgets.js" charset="utf-8"></script>

All she wanted to do was use the hover event (which lets you define 2 functions one for the mouseenter event and one for the mouseleave event) and start fading an element when you enter and stop and fade back to normal when you leave.  The problem was that her code wouldn't ever fade back.

```javascript
$(document).ready(function() {
    var $ul = $('ul').hover(function() {
        $(this).find('li:last').stop(true).fadeOut(1000);
    }, function() {
        $(this).find('li:last').stop(true).fadeIn(1000);
    });
});
```

Looking at the code it looks completely correct. The stop function stops all current animation on an element.  The parameter that she is setting to true tells jquery to clear the animation queue. Then she stars a new fade.  But it doesn't work!

I played around with a few things and decided to test out just using the animation function rather then the fade functions.

```javascript
$(document).ready(function() {
    $('ul').hover(function() {
        $(this).find('li:last').stop(true).animate({opacity:'0'},1000);
    }, function() {
        $(this).find('li:last').stop(true).animate({opacity:'1'},1000);
    });
});
```

It worked! I don't why animate works when the fadeIn/fadeOut doesn't, something I will need to get in to the code to find out.  Any one got a clue know why?
