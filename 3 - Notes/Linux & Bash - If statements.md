Tags: [[__Infrastructure_Engineering]] [[_Linux & Bash]]
#InfrastructureEngineering #LinuxBash 

# Introduction
Syntax:
```bash
if [ condition ]; then
	# commands to run if condition is true
else
	# commands to run if condition is false
fi
```
The condition must return either:
- true or false
- zero or non zero value

For example:
- `[X -eq 10]` condition compares environmental variable X to 10 and returns true or false.
- `[command]` condition runs a command which returns an exit code. If exit code = 0 that means true, any non zero value means false.