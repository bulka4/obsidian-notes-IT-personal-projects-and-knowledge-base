Tags: [[_Ray]], [[__Machine_Learning_Engineering]]
#Ray #MLEngineering 

# Easy of use vs control
Initialization of a Torch Distributed process group, preparing required processes and env vars is done automatically.

But that gives an extra abstraction layer so it is harder to reason about exactly where something is running, why something doesn't work.

Kubernetes-native solutions like Kubeflow Trainer ([[DeepSpeed - Kubernetes deployment with Kubeflow Trainer (TrainingRuntime CRD)|link]]) or MPI Operator ([[DeepSpeed - Kubernetes deployment with MPI Operator (MPIJob CRD)|link]]) advantages:
- Maximum control over pods, networking, security
- Easier to integrate with strict enterprise policies
- Less abstraction so easier to debug

**To explain:**
- **Slight overhead**
    - Actor scheduling, object store, serialization
- **Debugging complexity**
    - Stack traces may cross Ray + framework boundaries
# Developer experience
Ray Train advantages
- We work more with Python and less with YAML Kubernetes manifests
- Same code runs locally and on Kubernetes
# Performance
When we want to run a code, Ray needs to:
- Start on a node an actor ([[Ray Core - Actors|link]]) (Python worker process which will perform computations) and reserve for it CPUs / GPUs
- Save / read data in object store ([[Ray - Plasma object store|link]])
- Use serialization ([[Ray - Serialization|link]])
All of that takes time. 

So Ray is good for long jobs, where time needed for those operations is very small compared to the time of computations.
# Reusable environment
We deploy a Ray cluster (RayCluster CRD or Helm) once and we can use it to run many DeepSpeed jobs submitted as a Ray job.

Other solutions like Kubeflow Trainer ([[DeepSpeed - Kubernetes deployment with Kubeflow Trainer (TrainingRuntime CRD)|link]]) or MPI Operator ([[DeepSpeed - Kubernetes deployment with MPI Operator (MPIJob CRD)|link]]) allows to prepare environment and run only a single job on it.
# Function as execution unit
In Ray Train, a function (an actor ([[Ray Core - Actors|link]])) is a unit of execution that Ray can:
- Replicate
- Schedule
- Retry in case of failure
- Coordinate

For each function Ray Train can:
- Prepare env vars
- Execute different functions on different GPUs

In other tools like Kubeflow Trainer ([[Kubeflow Trainer - Introduction|link]]), we can do the same only for an entire script, not a single function from that script.

Being able to do this for a single function instead of an entire script gives us more flexibility.
# Cleaner scaling and resource handling
- Ray handles:
    - GPU allocation
    - one process per GPU
    - multi-node scaling
- You scale by changing:
    - number of Ray workers
    - GPUs per worker  
        —not rewriting launch commands.