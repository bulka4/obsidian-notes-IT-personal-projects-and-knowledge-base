Tags: [[__Cloud]], [[__DevOps]], [[__Distributed_computing]], [[__Infrastructure_Engineering]]
#Cloud #DevOps #DistributedComputing #DataEngineering 

# Introduction
The `spec.containers[i].command` parameter is a name of a binary (executable file, a program) to use and `spec.containers[i].args` are arguments for that command.
# Specifying command and arguments in pod's manifest
Command with arguments can be specified in a pod YAML manifest as:
```yaml
containers:
	- name: ...
	  command: ["command_part_1", "command_part_2"]
	  args: ["arg1", "arg2"]
```
or:
```yaml
containers:
	- name: ...
	  command:
		  - command_part_1
		  - command_part_2
	  args:
		  - arg1
		  - arg2
```

This is then executed in the container as:
```bash
command[0] command[1] args[0] args[1]
```
where `command[0]` is a binary and the rest (`command[1]`, `args[0]`, `args[1]`) are parameters for that binary.

So for example, if we want to run a Python script, that is to use:
- The `python` binary
- The `script.py` argument (name of the script to run)

we should specify in pod's manifest:
```yaml
command:
	- python
args:
	- script.py
```
or this would also work (less common):
```yaml
command:
	- python
	- script.py
```

but this would fail:
```yaml
command:
	- python script.py
```

because Kubernetes would treat the entire string `python script.py` as a name of a binary.
# Command that Kubernetes generates and run
Kubernetes generates and run the command:
```bash
execve(command[0], final_argv, env)
```
where `final_argv` is a combination of all commands and arguments:
```bash
final_argv = command + args = command[0] + ... + command[n] + args[0] + ... + args[n]
```

For example, if we have:
```yaml
command: ["python", "app.py"]  
args: ["--port", "8080"]
```
this will run in the container as:
```bash
execve("python", ["python","app.py","--port","8080"], env)
```
