# Events

Overview:

* [Event reference](https://developer.mozilla.org/en-US/docs/Web/Events)

APIs:

* [Event](https://developer.mozilla.org/en-US/docs/Web/API/Event)
* [Event properties](https://developer.mozilla.org/en-US/docs/Web/API/Event#properties)
* [EventListener](https://developer.mozilla.org/en-US/docs/Web/API/EventListener)
* [EventTarget](https://developer.mozilla.org/en-US/docs/Web/API/EventTarget)

## Event propagation

* [Bubbling and capturing](https://javascript.info/bubbling-and-capturing)
* [Event Propagation Explained](https://www.sitepoint.com/event-bubbling-javascript/)
* [(Video) Event Propagation Explained](https://www.youtube.com/watch?v=BtOrr7oTH_8)

Phases are accessible via the [Event.eventPhase](https://developer.mozilla.org/en-US/docs/Web/API/Event/eventPhase)
property and are represented as integers.

Phases:

1. *Capturing phase*: Every element above the target will be notified and can react to an event before the target does.
2. *Target phase*: We reach the actual element (target) where the event occured.
3. *Bubbling phase*: Every element above the target will be notified and can react to an event after the target does.

Event bubbling and capturing are two ways of propagating events that occur in an element that is nested within another
element, when both elements have registered a handle for that event. The event propagation mode determines the order in
which elements receive the event.

### Event bubbling

* [Event.bubbles](https://developer.mozilla.org/en-US/docs/Web/API/Event/bubbles)

Events bubble by default. Focus, blur, load and some others, don’t bubble up. During propagation, it is possible for a
listener to know if an event bubbles by reading the `Event.bubbles` property. 

## Creating events

* [Event() constructor - MDN](https://developer.mozilla.org/en-US/docs/Web/API/Event/Event)
* [CustomEvent() - MDN](https://developer.mozilla.org/en-US/docs/Web/API/CustomEvent/CustomEvent)
* [CustomEvent.detail - MDN](https://developer.mozilla.org/en-US/docs/Web/API/CustomEvent/detail): 

To add more data to the event object, the `CustomEvent` interface exists and the `detail` property can be used to pass
custom data.

## Event handling

* [Event handling (overview) - MDN](https://developer.mozilla.org/en-US/docs/Web/Events/Event_handlers)
* [EventTarget.addEventListener() - MDN](https://developer.mozilla.org/en-US/docs/Web/API/EventTarget/addEventListener)
* [EventTarget.removeEventListener()](https://developer.mozilla.org/en-US/docs/Web/API/EventTarget/removeEventListener)
* [Using onevent properties - MDN](https://developer.mozilla.org/en-US/docs/Web/Events/Event_handlers#using_onevent_properties)

Event-handlers are usually connected (or "attached") to various HTML elements using `EventTarget.addEventListener()`,
and this generally replaces using the old HTML event handler attributes.

`addEventListener()` works by adding a function or an object that implements `EventListener` to the list of event
listeners for the specified event `type` on the EventTarget on which it's called.

Further, when properly added, such handlers can also be disconnected if needed using
`EventTarget.removeEventListener()`.

```javascript
target.addEventListener(type, listener, options);
target.addEventListener(type, listener, useCapture);
```

### useCapture property (optional)

A boolean value indicating whether events of this type will be dispatched to the registered listener before being
dispatched to any EventTarget beneath it in the DOM tree. 

Events that are bubbling upward through the tree will not trigger a listener designated to use capture. If not
specified, useCapture defaults to false.

## Dispatching an event

* [EventTarget.dispatchEvent() - MDN](https://developer.mozilla.org/en-US/docs/Web/API/EventTarget/dispatchEvent)

Events can be triggered programmatically, such as by calling the `HTMLElement.click()` method of an element, or by
defining the event, then sending it to a specified target using `EventTarget.dispatchEvent()`.

## Event object in event handlers

The event object is automatically passed to event handlers to provide extra features and information.

### Event.target

* [MDN](https://developer.mozilla.org/en-US/docs/Web/API/Event/target)

Element that triggered the event.

The `target` property of the Event interface is a reference to the object onto which the event was dispatched. It is
different from `Event.currentTarget` when the event handler is called during the bubbling or capturing phase of the
event.

### Event.currentTarget 

* [MDN](https://developer.mozilla.org/en-US/docs/Web/API/Event/currentTarget)

Element that listens to the event.

The `currentTarget` read-only property of the Event interface identifies the current target for the event, as the event
traverses the DOM. It always refers to the element to which the event handler has been attached, as opposed to
`Event.target`, which identifies the element on which the event occurred and which may be its descendant.

## Event.preventDefault()

* [MDN](https://developer.mozilla.org/en-US/docs/Web/API/Event/preventDefault)

The `Event` interface's `preventDefault()` method tells the user agent that if the event does not get explicitly
handled, its default action should not be taken as it normally would be.

The event continues to propagate as usual, unless one of its event listeners calls one of:
* [stopPropagation()](https://developer.mozilla.org/en-US/docs/Web/API/Event/stopPropagation)
* [stopImmediatePropagation()](https://developer.mozilla.org/en-US/docs/Web/API/Event/stopImmediatePropagation)
either of which terminates propagation at once.

## AbortSignal

* [MDN](https://developer.mozilla.org/en-US/docs/Web/API/AbortSignal)
* [abort()](https://developer.mozilla.org/en-US/docs/Web/API/AbortController/abort)

A notable event listener feature is the ability to use an abort signal to clean up multiple event handlers at the same
time.

This is done by passing the same `AbortSignal` to the `addEventListener()` call for all the event handlers that you want
to be able to remove together.

You can then call `abort()` on the controller owning the `AbortSignal`, and it will remove all event handlers that were
added with that signal. 

