Tags: [[_Linux & bash]] [[__Operating_systems]] [[__Infrastructure_IT_tools]]
#Linux #OperatingSystems #InfrastructureITTools 

# PID
Every process get assigned a unique ID, denoted as PID (Process ID).
# Process tree
When a process A starts another process B, then process B becomes a child of the process A.
# Daemons
Daemons are background, long running processes.
# List processes
The ‘ps aux’ command shows all processes.

It returns a table with, among the others, those fields:
- User – who started the process
- Command – command used to start the process
- PID – id of a process

Any command we execute in shell starts a process and it will be visible in the table returned by the ‘ps’ command.

For example if we ran a Python script using a command:
- python script.py

Then after running ‘ps’ we will see ‘python script.py’ in the returned list as long as this script is running.
# Kill a process
We can use those commands to kill a process:
- kill \<process-id\>  kill a process
- kill -9 \<process-id\> - force killing a process

To get process ID we can use ‘ps aux’ command.
# Sending signals to processes
OS can send signals to processes (for example to stop the process). 