---
layout: post
title: jQuery UI 1.8 Widget Factory
categories:
- Posts
tags:
- javascript
- jQuery
- jQuery UI
- widget factory
comments: true
meta:
  dsq_thread_id: '157 http://blog.petersendidit.com/?p=157'
---
jQuery UI 1.8 is set to have its final release any moment now and with it comes an updated Widget Factory.  If you haven't used the widget factory before it's a great piece of code that does the generic jQuery plugin type of things for you.  You can read more about the [widget factory in this older post](http://blog.petersendidit.com/post/stateful-jquery-plugins-with-jquery-uis-widget-factory/) I did about it.

In jQuery UI 1.8 the Widget Factory gets a few very welcomed changes.  First default options are no longer defined outside of the widget, you now add an options property to the object you are passing $.widget and it will take care of merging your defined default options with the options the plugin gets initialized with.  This also means that in order to set global default options on the core jQuery UI widgets you need to now use $.ui.foo.prototype.options rather than $.ui.foo.defaults.  Also you no longer have to define getter methods like you did in 1.7.  In 1.8 any method that returns a value other then the plugin instance ( this ) or undefined it will assume it's a getter and return that value.  This is sweet because now you can define a method that is a chainable setter and a getter.  The option method now returns the full options hash when called without any paramaters.

The _init method has been renamed to _create and a new _init method was created.  Yes go ahead and read that again I had to do a double take too.  Basically _create is now called only once when the plugin is first initialized and should contain all the logic to set up the widget.  The new _init method gets called every time the plugin gets called without passing a name of a method.  So when you do: $('.selector').dialog({ height: 530 }); the first time both _create and _init get called.  If you call that again later only _init will be called.  This was created to fix a misunderstanding many people were having with the dialog plugin.  Many people were calling $('.selector').dialog(); and a dialog would open up, then later in the code they wold call the same thing and expect the dialog to popup. By having _init be called every time there is not a method provided it lets the dialog decide if it should open back up if it's called again.

The _setData method got renamed to _setOption to fit better with what is actually happening.  Destroy now handles removing all widget-namespaced events for the plugin that are bound to this.element or this.widget().  Meaning name space your events and you don't have to do the extra work of cleaning them up.

One very sweet thing is now you can create a new widget that extends an existing widget.  Just by doing something like: $.widget('myCustomAccordion', $.ui.accordion, { //all my custom methods }); which makes it very easy to create a custom widget that can expand upon and use functionality that is already in another jQuery UI plugin.  (The date picker still does not use the widget factory yet so it can not be extended like this).

There are a few other changes but these are the ones that perked my attention.  If you want more information check out the [Upgrade Guide for 1.8](http://jqueryui.com/docs/Upgrade_Guide#Widget_Factory) and check out [Scott Gonzalez's jQuery UI example code](http://docs.jquery.com/UI/Upgrade_Guide_18) for migrating the widget factory from 1.7 to 1.8.  If you're including the jQuery UI core in to your page and not using the jQuery UI Widget Factory to create your plugins you should start asking yourself, WHY?
