Tags: [[__Infrastructure_Engineering]], [[__Operating_systems]], [[__Infrastructure_IT_tools]]

# Introduction
Kernel manages hardware (CPU, RAM). It is a bridge between applications / processes and hardware.

Kernel tasks regarding processes:
- Start, stop and schedules processes
- Decides which process get resources (CPU, RAM) and when
- Keeps each process isolated in memory

Kernel tasks regarding file system management:
- Reads and writes files
- Map files to blocks on a physical disk

Kernel tasks regarding devices:
- Talks to hardware like keyboard, mouse, drive
- Routes data between devices and apps
- For example typing on a keyboard generates signals that kernel routes to terminal

Kernel tasks regarding security and isolation:
- Enforces user permissions
- Provides namespaces and cgroups

For example when we run a Python script then Kernel:
- Loads Python from disk
- Allocates memory
- Schedules it to run on the CPU
- Tracks when it finishes

#InfrastructureEngineering #OperatingSystems #InfrastructureITTools 