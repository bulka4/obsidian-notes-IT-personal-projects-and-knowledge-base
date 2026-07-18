Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# VM
VM virtualizes hardware. Each VM contains:
- Application
- Libraries
-  Guest Operating System
-  Hypervisor
- Host OS
- Hardware

The VM has its own:
- operating system kernel
- drivers
- filesystem
- virtual CPU
- virtual memory
# Container
A container virtualizes the operating system environment. It contains:
- Application
- Libraries
- Container
- Host OS kernel
- Hardware

Containers share the host kernel but have isolated:
- processes
- filesystem
- networking
- users
- resources

This is achieved using Linux features:

- **namespaces** → isolation
- **cgroups** → resource limits
# Other differences

| |VM|Container|
|---|---|---|
|Virtualizes|Hardware|OS|
|Has own kernel|Yes|No|
|Size|GBs|MBs|
|Startup|Seconds/minutes|Milliseconds/seconds|
|Isolation|Stronger|Weaker|
|Density|Fewer per server|Many per server|
|Runs different OS|Yes|Usually no|
