---
layout: post
title: cssHooks in jQuery 1.4.3
categories:
- Posts
tags:
meta:
  dsq_thread_id: '182413355'
---
jQuery 1.4.3 brought us a complete rewrite of the CSS module.  The main focus of this rewrite was to add extensibility. Along with some [nice speed-ups in getting styles](http://www.flickr.com/photos/jeresig/5079106854/), the CSS module of jQuery now let you extend the functionality of .css() and .animate().  It allows this by adding cssHooks.

cssHooks allow you to "hook" in to how jQuery gets and sets css properties.  This means that you could create a cssHook to help normalize differences between browsers, or to add some missing functionality from the stock jQuery.fn.css().

[Brandon Aaron](http://brandonaaron.net/) has been doing some work, along with others, to create a [collection of cssHooks](https://github.com/brandonaaron/jquery-cssHooks).  They currently have:

* margin and padding
* backgroundPosition, backgroundPositionX, backgroundPositionY
* boxShadow, boxShadowColor, boxShadowBlur, boxShadowX, boxShadowY

And I am sure there more to come.

Defining a new cssHook is very easy

```javascript
	$.cssHooks['cssproperty'] = {
		get: function( elem, computed, extra ) {
			// Handle getting the css property here
		},
		set: function( elem, value ) {
			// Handle setting the css value here
		}
	};
```

Very simple and easy. To allow your new cssHook to be used with .animate() all it takes is (for simple number value animations):

```javascript
	$.fx.step [ "cssproperty" ]  = function( fx ) {
		$.cssHooks [ "cssproperty" ].set( fx.elem, fx.now + fx.unit);
	};
```

Will be interesting to see what other cssHooks show up.
