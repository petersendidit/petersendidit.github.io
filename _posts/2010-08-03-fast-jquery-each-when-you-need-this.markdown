---
layout: post
title: Fast jQuery each when you need $(this)
categories:
- Posts
tags: []
comments: true
meta:
  dsq_thread_id: '165 http://blog.petersendidit.com/?p=165'
---
Most of the time you use the jQuery $.fn.each function you end up doing $(this) inside the function that is getting looped.  You want access the jQuery magic in your loop.  It's always seemed weird to me that $.fn.each didn't pass your function a jQuery version of the element, since you already selected it in order to do the $.fn.each call.  Well [James Padolsey](http://james.padolsey.com/) started playing and created a [quickEach plugin](http://gist.github.com/500145) that passes in a jQueryized version of this.  Then [Ben Alman](http://benalman.com/) started playing with it and ended up with a [$.fn.each2](http://benalman.com/projects/jquery-misc-plugins/#each2) plugin. It is optimize just for the case where you need a jQueryized version of this in the loop, it is [slower then the built in $.fn.each function](http://jsperf.com/jquery-each2-vs-each) when you don't.

```javascript
// jQuery each2 plugin usage:
$('a').each2(function( i, jq ){
	this; // DOM element
	i; // DOM element index
	jq; // jQuery object
});

// jQuery core .each method usage:
$('a').each(function( i, elem ){
	this; // DOM element ( this === elem )
	i; // DOM element index
	$(this); // jQuery object
});
````
