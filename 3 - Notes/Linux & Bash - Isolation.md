Tags: [[__Infrastructure_Engineering]] [[_Linux & Bash]] [[_Software_Engineering]]
#InfrastructureEngineering #LinuxBash #SoftwareEngineering 

# Introduction
Isolation is the broader concept of separating resources or execution environments so that different processes, users, or systems do not interfere with each other.

Sandboxing ([[Linux & Bash - Sandboxing|link]]) is one way to achieve isolation.
# Examples
## Process isolation
Processes have separate:
- memory spaces
- file descriptors
- execution contexts

One process normally cannot directly access another process's memory.
## User isolation
Different Linux users have different permissions:
```
User A cannot access User B's files.
```
## Container isolation
Docker containers isolate:
- processes
- filesystems
- networks
- users (optionally)

using Linux namespaces and cgroups.
## Virtual machine isolation
VMs provide even stronger isolation:
```
Application
    ↓
Container
    ↓
Host OS
```
vs.
```
Application
    ↓
Guest OS
    ↓
Hypervisor
    ↓
Host OS
```

A VM has its own kernel, giving stronger isolation.
## Network isolation
Examples:
- Kubernetes Network Policies
- VPCs/VNets
- Firewalls

Services may be unable to communicate unless explicitly allowed.
## Data isolation
Databases may isolate:
- tenants
- transactions
- users

For example, transaction isolation levels in databases are another form of isolation.