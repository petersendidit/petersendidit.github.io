---
layout: post
title: Drag table row to a div with jQuery
categories:
- Posts
tags:
- demo
- dragable
- dropable
- jQuery
- jQuery UI
comments: true
meta:
  dsq_thread_id: '83 http://blog.petersendidit.com/?p=83'
---
One of projects I am working on has a long list of classes in a catalog.  These classes are listed on the screen in a table which is sortable and filterable.  Users search through these classes trying to find ones that they want to register for, when the find one they can click on the "add to cart" button in that classes row.  One of the requirements that I was given for this listing was that users should also be able to drag a row to the cart. jQuery UI's draggables works very nicely but after doing a quick proof-of-concept test I found that draggables don't work on on table rows very well.  I couldn't get jQuery UI to drag anything.

If you check out the [documentation](http://jqueryui.com/demos/draggable/) you will find a option for a "helper".  This option can either be set to a string ('clone' or 'original') or you can provide a function which returns the helper object.  So I wrote up some code to create a div with the selected row in a new table.

```javascript
helper: function(event){
	return $('<div class="drag-cart-item"><table></table></div>')
		.find('table').append($(event.target).closest('tr').clone()).end().appendTo('body');
},
```

Then all you need to do is set up a dropable area that knows how to handle that helper.

```javascript
('#cart').droppable({
	drop: function(event, ui) {
		var classid = ui.helper.find('tr').attr('id');
		var name = ui.helper.find('.name').html();
		$('#cart .selected').append('<li id="'+classid+'">'+name+'</li>');
	}
});
```

Updated Demo using jQuery 1.4.3 and jQuery UI 1.8.5

[Check out the working demo](http://jsfiddle.net/petersendidit/cZare/2/show/)
