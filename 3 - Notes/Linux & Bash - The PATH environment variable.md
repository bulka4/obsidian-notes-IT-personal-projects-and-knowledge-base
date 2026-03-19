Tags: [[__Infrastructure_Engineering]] [[_Linux & Bash]]
#InfrastructureEngineering #LinuxBash 

# Introduction
The `PATH` environment variable contains directories in which shell looks for executable files we want to execute. It is of the format:
```bash
PATH=path_1:path_2:...:path_n
```

When we run `command`, then shell will search for this executable file in directories given by paths from `PATH` from left to right, so it will try to run `path_1/command`, `path_2/command` etc. until the command works or until the end of `PATH` is reached.