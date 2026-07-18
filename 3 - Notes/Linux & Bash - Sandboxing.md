Tags: [[__Infrastructure_Engineering]] [[_Linux & Bash]] [[_Software_Engineering]]
#InfrastructureEngineering #LinuxBash #SoftwareEngineering 

# Introduction
**Sandboxing** is a security technique that runs a program in an **isolated, restricted environment**, limiting what resources it can access.

The idea is:
> "Even if the program is buggy or malicious, it should not be able to damage the rest of the system."
# Examples of restrictions
A sandbox may limit access to:
- files and directories
- network connections
- devices
- processes
- system calls
- CPU and memory usage
# Linux examples
## File isolation
A process can only see certain directories.
## User isolation
Run the process as a low-privilege user:
```
useradd myservice
```
## Container isolation
Docker containers are a form of sandboxing using:
- namespaces
- cgroups
- capabilities
- seccomp
- AppArmor/SELinux
## System call filtering
`seccomp` can block dangerous system calls:
```
Process cannot:
- mount filesystems
- load kernel modules
- reboot machine
```