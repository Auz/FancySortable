FancySortable
===========

FancySortable is a mootools class which creates a sortable list with fancy effects.


Demo
----

See: http://jsfiddle.net/auzz/yXTfv/


Features
--------

* Fancy hover effects which show and hide 'gaps' between the list to indicate the future position should the user release the mouse.
* Adds an element which expands between list items, so this 'gap' can be styled.
* Ghosted dragged item and/or original item.
* Event delegation for performance.
* Ability to use this class with other 'droppable' items using onDrop event, and other Drag.Move events (see below).


How to use 
----------

FancySortable takes three parameters, the parent element (or id), a selector for each item 
(relative to the parent), and an optional options object. 


The basic use case:
A list of elements exist in on the page contained by a parent element. 

	<div id='listwrap'>
		<div class='listitem'>The Shawshank Redemption (1994)</div>
		<div class='listitem'>The Godfather (1972)</div>
		...
	</div>

The list would then be made sortable with this:

	new FancySortable('listwrap', '.listitem');

Using a handle:
Similar to above, but adding a handle element...

        <div id='listwrap'>
                <div class='listitem'><div class='handle'></div>The Shawshank Redemption (1994)</div>
                <div class='listitem'><div class='handle'></div>The Godfather (1972)</div>
                ...
        </div>

The call would now be:

	new FancySortable('listwrap', '.listitem', {'handleSelector':'.handle'});

Or to do something on the sort event:

	new FancySortable('listwrap', '.listitem', {
		'handleSelector':'.handle',
		'onSort': function(item, i, ind) {
			console.log('item moved from '+ind+' to '+i, item);
		}
	});

Options
-------

* handleSelector - A selector, relative to the parent, for the handle. Defaults to nothing, and uses the whole item as a draggable element
* droppableclass - A class which marks elements as able to receive droppable items. See Drag.Move. Default: 'droppable'
* hoverClass - A class to add to a list item when it is being hover over. Default: 'drag-over'
* betweenClass - Class to add to elements inserted to make gaps to indicate the drop position. default: 'between-item'
* betweenOpenClass - Class which is added to the between element when they are opened. default: 'open'
* sortOverlayClass - Class to use on the invisible overlays. Default: 'sortoverlay'
* betweenEl - Element tag name to use on the between elements. Defaults to the same as the list item.
* expandHeight - Number of px high to make the gap between items when hovered over. 
* hoverDuration - Number of milliseconds to make the effects last for on hovers. Default: 300 ms
* moveDuration - Number of milliseconds for the move effect. Default: 700ms.
* dragOpacity - Opacity, from 0 to 1, to make the the dragging element.
* origOpacity - Opacity, from 0 to 1, to make the original item in the list.

Events
------

* onBeforeStart: function(Event, item){}, - On mouse down on an item.
* onStart: function(Drag, item, clone){}, - Fired when the user clicks on an item or handle, just after Drag.start().
* onMoved: function(item, i, ind){}, - Fired when the list has been re-ordered. 'i' is the new index (from 0 to length+1) and 'ind' is the old position.
* onHoverOver: function(dragging, target, i, ind){}, - When an item ('dragging': index 'ind') is dragged over another list item (index i).
* onHoverOut: function(dragging, target, i, ind){}, - When an item ('dragging': index 'ind') leaves the area of a list item (index i).
* onSort: function(){}, // Fired when the list is sorted by the user, and the list of items and their indexes are recalculated.

The following events are roughly analogous to events passed from Drag.Move, and allow one to use other 'droppable' elements besides re-ordering.

* onDrop: function(dragging, item){}, - The item was dropped on a 'droppable' element, but it wasn't a FancySortable droppable.
* onMissed: function(dragging, item){}, - The user dropped the item and didn't hit any droppables (dragged item returns to original position).
* onCancel: function(dragging, item){}, - The drop even was canceled (it wasn't dragged far enough).
* onEnter: function(dragging, target){}, - The user dragged an item over a droppable.
* onLeave: function(dragging, target){}, - The user left a droppable element.


Caveats
-------

* This class will insert elements between list items. This may cause problems when using ol's or nth-child selectors.
* This class adds position relative to the parent element (first parameter), which may cause problems in IE6, or other layout issues.
* This class adds overflow hidden to each item in order to 'slide' them out. This may cause things to display incorrectly or jump if you have non-cleared floating elements inside each list item.
* Standards modes are required for drag to work correctly. (see Drag.Move)

