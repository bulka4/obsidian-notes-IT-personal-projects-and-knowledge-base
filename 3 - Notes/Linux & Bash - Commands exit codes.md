Tags: [[__Infrastructure_Engineering]] [[_Linux & Bash]]
#InfrastructureEngineering #LinuxBash 

# Introduction
Every bash command returns an exit code. Exit code = 0 means success and any other value means some kind of error.

We can access an exit code of a command by using $? after that command, for example:
```
ls /nonexistent
echo $? # Outputs a non-zero number because the directory doesn't exist
```