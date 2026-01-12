Tags: [[__Web_Development]]
#WebDevelopment 

# Introduction
ASGI server is a software which runs an application defined by an ASGI web framework ([[ASGI web framework|link]]).

It works like that:
- Starts one or more processes which uses our app's code
- Listens for requests from clients
- Translates requests into ASGI calls (calls an ASGI callable with proper arguments)
- Executes our app's code to handle each request.