Tags: [[__Infrastructure_Engineering]] [[_Linux & Bash]]
#InfrastructureEngineering #LinuxBash 

# Introduction
We can isolate processes on Linux, such that they can:
- Use only a specific amount of resources (CPU, RAM)
- See and access only a specific files, other processes

For managing which resources processes can use, we are using cgroups ([[Linux & bash - cgroups|link]]).

For managing what processes can see we are using namespaces ([[Linux & bash - Namespaces|link]]).