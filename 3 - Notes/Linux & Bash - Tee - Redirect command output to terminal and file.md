Tags: [[__Infrastructure_Engineering]] [[_Linux & Bash]]
#InfrastructureEngineering #LinuxBash 

# Introduction
The `tee` command redirects an output of another command to both a terminal and a file. Example use cases:
- `Command | tee filename` - Save an output of the command in the given file and also write it in a terminal.
- `Command | tee filename | another_command` – save an output of the command in the given file and also redirect that output to another command.