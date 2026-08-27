Tags: [[_JavaScript]] [[__Programming_languages]]
#JavaScript #ProgrammingLanguages 

# Introduction
The `EventEmitter` is a class for emitting events and performing specific operations when an event occurs. Event is just a named notification, for example:
```javascript
const EventEmitter = require('events');

const emitter = new EventEmitter();

// Define what to do when the event 'hello' occurs
emitter.on('hello', () => {
    console.log('Hello event happened!');
});

// emit the 'hello' event
emitter.emit('hello');
```

So the `on()` method is specifying what happens when the same `EventEmitter` object emits a specific event. 
# Events can carry data
An event doesn't have to be just a notification.

You can send arguments:
```javascript
emitter.on('userCreated', (user) => {
    console.log(user.name);
});

emitter.emit('userCreated', {
    name: 'Marcin'
});
```
The emitter passes the argument to the listener.
# Questions
- the same emitter object sends events and listens to them? can there be two emitters sending events to each other?