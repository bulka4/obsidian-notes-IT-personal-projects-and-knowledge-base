Tags: [[__Software_Engineering]]
#SoftwareEngineering 

# Introduction
Optimistic Concurrency Control (OCC) is a concurrency pattern to deal with the race condition ([[Software Engineering - Concurrency - Race conditions|link]]) problem.

It can help with preventing lost updates where two clients read the same data and update it independently. One update overwrites the other, so the other update is lost.

Example: Two users edit the same task / document.
# How it works
In this pattern:
- The client saves information about the version of the latest read data
- When the client requests to update data, it sends together with the request information about the latest read value
- The server, before updating data, compares the actual version of the data that is requested to be updated with the version provided in the request
- If the version provided in the request is smaller, then data is not updated but instead the server returns an error with a message indicating that this data has been updated by another client since this client read it last time

This is useful for example when the client is a user using a frontend app. Frontend can store information about the latest read value.

For example, we can have a scenario where:
- user A, using the frontend, reads the document X and the frontend saves information about its version
- another user B, using this frontend, updates the document X
- user A didn't see the updated document X yet (didn't read it)
- user A sends a request to update the document X
- the server returns an error indicating that the document X has been updated since the last time user A read it

User A didn't see updates from the user B, so if we just accept update from the user A, all the changes done by the user B will be lost and user A will not see this.