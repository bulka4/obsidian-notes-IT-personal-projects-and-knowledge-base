Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
An I/O event is both:
- A notification that some event has happened that changed the state ([[Backend Engineering - Distributed systems - State|link]]) of an I/O resource ([[Software Engineering - I-O resources|link]]) (such as a network socket, file, or device) in a way that affects the ability to perform an I/O operation
- The event itself that the notification is about.

That changed state can be caused for example by such evets as:
- socket has received data
- socket is ready to accept data
- file read completed
- connection closed
- User clicked on a button