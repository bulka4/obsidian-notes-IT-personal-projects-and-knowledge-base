Tags: [[__Infrastructure_Engineering]] [[_Linux & Bash]]
#InfrastructureEngineering #LinuxBash 

# Introduction
Using the `head -n n` command we can get the first n lines of the text.

We can combine this with other commands to get only the first lines from the output of that command.

For example, if the logs_command is a command returning some logs, we can get the first 200 lines of those logs this way:
- `logs_commang | head -n 200`