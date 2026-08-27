Tags: [[_JavaScript]] [[__Programming_languages]]
#JavaScript #ProgrammingLanguages 

# Introduction
1. [[JavaScript - Benefits and drawbacks]]
2. [[JavaScript - Events]]
	1. [[JavaScript - EventEmitter]]
3. [[JavaScript - Importing modules]]
	1. [[JavaScript - Caching modules]]
4. [[JavaScript - User authentication]]
	1. [[JavaScript - User authentication - Passport library]]

# Topics to explore
1. EventEmitter
   ├── 2.1 EventEmitter concept
   ├── 2.2 Creating an EventEmitter
   ├── 2.3 .on()
   ├── 2.4 .emit()
   ├── 2.5 .once()
   ├── 2.6 .off() / .removeListener()
   └── 2.7 Event arguments

2. Event lifecycle
   ├── 3.1 Registering a listener
   ├── 3.2 Emitting an event
   ├── 3.3 Calling listeners
   └── 3.4 Removing listeners

3. Node.js EventEmitter
   ├── 4.1 Objects that extend EventEmitter
   ├── 4.2 Custom events
   ├── 4.3 Built-in Node.js events
   └── 4.4 Error events

4. Asynchronous events
   ├── 5.1 Events and the event loop
   ├── 5.2 Synchronous listener execution
   ├── 5.3 Asynchronous operations triggering events
   └── 5.4 Events vs callbacks

5. Events vs Promises
   ├── 6.1 One-time result → Promise
   ├── 6.2 Repeated notifications → Event
   └── 6.3 Using events and Promises together

6. Browser events
   ├── 7.1 DOM events
   ├── 7.2 addEventListener()
   ├── 7.3 Event object
   ├── 7.4 Event propagation
   │   ├── Capturing
   │   └── Bubbling
   └── 7.5 Preventing default behavior

7. Practical Node.js events
   ├── 8.1 Network/socket events
   ├── 8.2 Stream events
   ├── 8.3 Process events
   └── 8.4 Library-specific events
       └── Redis client events