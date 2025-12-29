Tags: [[__Machine_Learning_Engineering]]

# Introduction
We can assign multiple replicas to one actor, that is one worker process. It is controled using the max_ongoing_requests parameter in the deployment.

If we compare this to running each replica on a separate actor:
- We have more actors so more processes. Server is more burdened.

If we compare this to running one replica on one actor:
- Multiple replicas can receive multiple requests at the same time (each replica is receiving requests at the same time). Those requests are added to a queue and they are waiting there to be executed by the worker process.
- Received requests can be batched and processed together what is sometimes more beneficial (for example making a prediction with ML model for multiple inputs at the same time).
- Received requests can be processed at the same time if they are asynchronous functions.

#MLEngineering 