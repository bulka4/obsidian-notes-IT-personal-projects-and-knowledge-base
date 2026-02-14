Tags: [[__Infrastructure_Engineering]] [[_Linux & Bash]]
#InfrastructureEngineering #LinuxBash 

# Introduction
We can redirect / save an output of a command:
- To a file:
	- `Command > file` – overwrite a file if it exist
	- `Command >> file` – append to a file if it exists
- To a variable: `X=$(command)`
- To another command:
	- Command1 | command2 – output of the command1 becomes an input for the command2
- Redirect the standard output (stdout) to one location and standard error (stderr) to another location:
	- `Command > filename1.txt > filename2.txt`
- Redirect stdout and stderr to the same location:
	- `Command > filename.txt 2>&1`
- Hide the stdout and stderr (redirect it to the ‘black hole’):
	- `Command > /dev/null 2>&1`