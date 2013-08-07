---
layout: post
title: Stateful jQuery plugins with jQuery UI's widget factory
categories:
- Posts
tags:
- javascript
- jQuery
- jQuery UI
- plugin
- stateful
- widget factory
comments: true
meta:
  dsq_thread_id: '126 http://blog.petersendidit.com/?p=126'
---
There are many different formats for jQuery plugins, many of the formats are not designed for stateful plugins.  What is a stateful plugin? A plugin that keep track of what the state of the plugin is and lets you call methods and change properties even after the plugin as been initialized.  All of [jQuery UI](http://jqueryui.com/)'s plugins are stateful (as of version 1.7.2), part of the jQuery UI core is a "[Widget Factory](http://docs.jquery.com/UI_Developer_Guide#The_widget_factory)" which makes it very easy to quickly make a stateful plugin.

Below is an example of a plugin created with the [jQuery UI widget factory](http://jqueryui.pbworks.com/Widget-factory).

```javascript
$.widget('namespace.pluginName', {
	_init: function() {
		// stuff that is called on initialization of the plugin

		//this.options a combination of the defualt options and the ones passed in during the plugin initialization
		if (this.options.foo) {
			//this.element is the element that the plugin was called on
			this.element.fadeOut();
		}
	},
	_privatemethod: function() {
		//private internal function
		//private functions should be named with a leading underscore
		//will only be able to be called from inside the plugin
	},
	publicmethod: function() {
		//this is a public fuction that can be called outside of the plugin

		//calling the private method from inside the public method
		this._privatemethod();
	},
	value: function() {
		//this is a public function that is defined as a getter
		//meaning it returns a value not a jquery object
		return this.options.foo;
	},
	destroy: function() {
		$.widget.prototype.apply(this, arguments); // default destroy
		// this is where you would want to undo anything you do on init to reset the page to before the plugin was initialized.
	}

}));

$.extend($.namespace.pluginName, {
	getter: 'value',
	defaults: {
		option1: 'bar',
		foo: true
	}
});
```

With this you can call the following to initialize the plugin

```javascript
$('#myelement').pluginName();
```

To call the publicmethod function you can now do this after initializing the plugin:

```javascript
$('#myelement').pluginName();
$('#myelement').pluginName('publicmethod');
```

This makes it very easy to create a stateful jQuery plugins very quickly. All you need is the core of jQuery UI, but most people already have the whole jQuery UI package on their page.
