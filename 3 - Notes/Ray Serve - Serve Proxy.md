Tags: [[__Machine_Learning_Engineering]]

# Introduction
For every deployment ([[Ray Serve - Deployment|link]]), Ray Serve creates a proxy which is a process (HTTP gateway, Starlette ASGI) which receives requests from clients and forwards them to a proper replica ([[Ray Serve - Replica|link]]) which will handle them (execute deployment's code) and send back a response.

#MLEngineering 