Tags: [[__Cloud]], [[__DevOps]], [[__Distributed_computing]], [[__Infrastructure_Engineering]]
#Cloud #DevOps #DistributedComputing #DataEngineering 

# Introduction
The mpirun command is used to start selected processes (MPI job ([[MPI job|link]])) with MPI runtime libraries preloaded what allows those processes to participate in MPI ([[MPI (Message Passing Interface)|link]]) communication. 

It is almost always used together with another command:
```
mpirun some_command ...
```
where `some_command` starts processes and `mpirun` allows them to use MPI communication.

It takes care of the following tasks:
- Performs preparations so those processes can later initialize other communication frameworks like NCCL ([[NCCL|link]])
- Assigns to each process a global and local rank which are unique identifiers of those processes
- It knows hostnames, ports and ranks, and builds a process tables describing which processes lives on which server allowing for communication
- Performs additional configurations (like opening TCP sockets) which enable those processes to communicate
- Sets up env vars which are then used for communication
# Questions
- 