Tags: [[__Infrastructure_Engineering]] [[_Linux & Bash]]
#InfrastructureEngineering #LinuxBash 

# Introduction
When a process creates a new folder, what permissions will be set up for that folder depends on the default Linux permissions and umask used by the process.

New folder will get the default permissions without permissions which umask removes.

So actual permissions which will be set up for a new folder are calculated like this:
```bash
Default permissions - umask = actual permissions
```
So if `Default permissions=777`, `umask=022`, then actual permissions which a new folder will receive will be `755`.