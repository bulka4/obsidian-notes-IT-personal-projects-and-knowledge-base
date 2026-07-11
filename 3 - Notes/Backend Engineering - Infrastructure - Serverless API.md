Tags: [[_Backend_Engineering]]
#BackendEngineering 

# Introduction
Serverless APIs are APIs where we write and deploy backend functions, but we do not manage the servers that run them.

The cloud provider handles:
- provisioning servers
- scaling
- availability
- operating system updates
- server maintenance

We only provide the code.

Usually, we pay per execution (for time when API function is executing).
# Benefits
- Easy scaling and faster development - No manual server management.
- Good for irregular traffic - We pay only when function runs
# Drawbacks
- Cold starts - If a function has not run recently, the first request can be slower (as environment needs to start)
- Execution limits - Functions often have limits - maximum execution time, memory limits,  temporary storage limits
- Less control - We can't tune operating system, hardware or networking details