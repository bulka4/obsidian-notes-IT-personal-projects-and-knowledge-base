Tags: [[__Infrastructure_Engineering]] [[_Linux & Bash]]
#InfrastructureEngineering #LinuxBash 

# Introduction
When we are defining environmental variables we can use the export statement:
- `Export X=1`

This way the specified variable will be accessible in all the subprocesses (compiled programs) which we run after defining that variable.

Here are examples of subprocesses using environmental variable:
- Example 1. A bash subprocess:
	- `export X=1`
	- `bash -c 'echo $X'`
- Example 2. A Python subprocess:
	- `export X=1`
	- `python3 -c 'import os; print(os.environ["X"])'`