# Event Listener System

The event listener system allows to attach an unlimited number of handler functions to arbitrary "events" and to dispatch (call the handlers) events at any time, while preserving the RID (attached player) and passing arguments (which is impossible with donpcevent()).

## Creating events
### Manually creating events

Creating events is done automatically but can also be done manually if desired. Internally, the event listener system uses hash tables to store the listeners. You can create events by simply creating hash tables manually.

```c
.myEvent = htnew();
```

### Automatically creating events

An event will be created automatically when adding a listener to an event if it doesn't already exist. If using a variable, the event will be scoped with the same scope as the variable. If using a string, the event will be globally scoped.

```c
// scoped:
addEventListener(.myScopedEvent, ...);

// global:
addEventListener("myGlobalEvent", ...);
```


## Adding event listeners

Event listeners are local NPC functions marked as `public`. Adding an event listener will register the target function of the current NPC as handler for the specified event. It is possible to register a handler in another NPC using the syntax `npcName::function` as second argument.

```c
public function myListener {
    // this will be called when "myEvent" is fired
}

addEventListener("myEvent", "myListener");
```

## Dispatching events

Dispatching an event will fire (execute) all handlers that *listen* to this event and pass along any argument specified. The arguments can be accessed normally with `getarg(...)` in the handler function.

```c
// fire the handlers for myEvent and pass the arguments "foo", 42, "bar"
dispatchEvent("myEvent", "foo", 42, "bar", ...);
```

Handlers are called **sequentially** one at a time. If one of the handlers reaches a script terminator (end, close, ...), the rest of the handlers won't be called and execution will end.
