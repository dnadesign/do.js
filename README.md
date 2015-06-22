# do.js
jquery event handler

Rather than creating a lot of jquery.on functions which are difficult to trace we created a simple wrapper for helping us track down
which events were being fired and listened to.

## Firing an event

```
DO.Fire(eventName, data);
```

## Listening to an event:

```
DO.Subscribe(eventName, function(event, jQuery, data){
  // do things here
});
```

## Naming
We recommend creating events with a prefix of the module or sub system the events comes from.
* app:ready
* app:loaded
* carousel:next
* carousel:previous
* etc

## One time events
Since some events can only happen once in a page event history (ready, loaded) you can denote an event as a one time event:

```
DO.Fire('app:ready', [], true);
```

This means that if another bit of javascript subscribes to that event after it's already fired, do will immieditely trigger 
the callback as if it's fired right now.

## Debugging
Setting `DO.Debug = true;` means that all subscribe and fire events will be pushed to the console so you can easily see what
is happening, in which order, and which elements are listending and firing which events.

## Getting started
We suggest initially adding the following to your js
```
jQuery(document).ready(function(e) {
	DO.Fire('app:ready', [], true);
});

jQuery(window).load(function(e) {
	DO.Fire('app:loaded', [], true);
});

DO.Subscribe('app:ready', function(e, $) {
 // do stuff
});
DO.Subscribe('app:loaded', function(e, $) {
 // do more different stuff
});
```
