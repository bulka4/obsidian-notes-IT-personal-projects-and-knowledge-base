Tags: [[__Infrastructure_Engineering]] [[_Linux & Bash]]
#InfrastructureEngineering #LinuxBash 

# Introduction
It is a tool for filtering text. For example we can:
- Filter a content of a file. Below command shows only those lines from the file.txt file which contains ‘error’ string:
	- `Cat file.txt | grep “error”`
- Filter output of some command. Below command shows only running processes related to nginx:
	- `ps aux | grep nginx`