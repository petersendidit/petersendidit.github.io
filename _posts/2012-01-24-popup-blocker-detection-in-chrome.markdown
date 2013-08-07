---
layout: post
title: Popup blocker detection in Chrome
categories:
- Posts
tags:
- browser
- chrome
- javascript
- popup
comments: true
meta:
  dsq_thread_id: '551832401'
  dsq_thread_id: '180 http://blog.petersendidit.com/?p=180'
---
Chrome has a popup blocker just like all good browsers, protecting us from annoying advertisements for face cream and "enhancements". But Chrome's popup blocker acts a little different than other browsers. Most browsers do not create the window when window.open is called. Window open returns undefined and you know that your popup was blocked. Chrome does it differently, it passes you a window object. Not only does it create the window object it actually [loads the page](http://code.google.com/p/chromium/issues/detail?id=3477)! So how do you figure out if Chrome blocked a popup?! From some testing and playing I found that after the popup you can do something like:

```javascript
newWindow.onload = function () {
	console.log('The popup is'  + (newWindow.innerHeight > 0 ? 'open' : 'blocked') );
}
```
(Thanks to [@rem](https://twitter.com/rem) for refining this with me)

After the popup is created you bind to the onload event and check the windows innerHeight. If the innerHeight of the popup window is greater than 1 then popup wasn't blocked, if its not well then Chrome blocked you.

My original attempt at this used a setTimeout because I wanted to allow for Chrome to block the popup, then the user react to the block and open it. I have combinded my original attempt with [@rem](https://twitter.com/rem)'s solution and came up with this: [http://jsfiddle.net/petersendidit/8gLyz/1/](http://jsfiddle.net/petersendidit/8gLyz/1/)
