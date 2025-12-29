Tags: [[__Machine_Learning_Engineering]]

# Introduction
Ray Serve is a framework for serving long running Python services that can be accessed via HTTP, gRPC, or directly through Ray APIs.

Usually it is used to serve ML models as Rest APIs. For example we can define REST API endpoints using FastAPI, Ray Serve will be running a proxy which will be receiving HTTP requests, and FastAPI will be handling those requests.

We can also expose plain Python functions/classes accessible through Ray APIs.

When we make a request to a Ray Serve endpoint, the corresponding Python code runs on a Ray cluster, in worker processes assigned to actors.

#MLEngineering 