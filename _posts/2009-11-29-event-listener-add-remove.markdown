---
layout: post
title: Event listener add remove add remove . . . .
categories:
- Posts
tags:
- javascript
- jQuery
comments: true
---
Something I have seen in many people have problems with on Stack Overflow, jquery's google group, and forums is people who are assigning an event listener and then because something happens, normally because the thing is being animated, they kill the event listener and then once the animation is finished they add it back. You end up mucking with the element far more then you really need to.

Example of what I am seeing:

```javascript
var doclick = function(){
    $(this).animate({'left':200},function(){
        $(this).bind('click',doclick);
    }).unbind('click');
};
$('li').bind('click',doclick);
```

You have duplicated code and will get very messy very quickly as more functionality gets added.

It would be much better to check if the thing is animated and if so just exit:

```javascript
var doclick = function(){
    if ($(this).is(':animated')) return false;
    $(this).animate({'left':200});
};
$('li').bind('click',doclick);
```

No adding and removing the event listeners just decide if you really care if was clicked.
It doesn't event need to be if its animated you can just use a flag to decide:

```javascript
var flag = false;
var doclick = function(){
    if (flag) return false;
    $(this).animate({'left':200});
};
$('li').bind('click',doclick);
$('div.stopclicks').bind('click',function(){
    flag = true;
});
```
