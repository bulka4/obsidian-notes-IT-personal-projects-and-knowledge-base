Tags: [[__Infrastructure_Engineering]] [[_Linux & Bash]]
#InfrastructureEngineering #LinuxBash 

# Grep
It is a tool for filtering text. For example we can:
- Filter a content of a file. Below command shows only those lines from the file.txt file which contains ‘error’ string:
	- `Cat file.txt | grep “error”`
- Filter output of some command. Below command shows only running processes related to nginx:
	- `ps aux | grep nginx`
# Head
Using the `head -n n` command we can get the first n lines of the text.

We can combine this with other commands to get only the first lines from the output of that command.

For example, if the logs_command is a command returning some logs, we can get the first 200 lines of those logs this way:
- `logs_commang | head -n 200`
# Tee
The tee command redirects an output of another command to both a terminal and a file. Example use cases:
- `Command | tee filename` - Save an output of the command in the given file and also write it in a terminal.
- `Command | tee filename | another_command` – save an output of the command in the given file and also redirect that output to another command.
# Echo
The `echo` command prints a text. It can be used for example in order to save a text into a file.
# Ls
`ls` command is used for listing files contained in a directory and checking their permissions. Syntax:
- `ls [options] folder_path`

Where folder _path is a path to the folder from which we want to list the content (files and folders).

Popular options:
- -l – show permissions, owner, size etc.
- -a - show all file, including the hidden ones (which name starts with a dot ‘.’).
- -d – Get information about the directory itself (given by the folder_path), not its content.
# Mkdir
Create a folder. Syntax:
- `mkdir [options] folder path`

Popular options:
- -p – Create the entire path. For example if we run ‘mkdir -p folder1/folde2 and both folders doesn’t exist yet, then it will create both of them.
# Sysctl
It is used to view and modify kernel parameters without rebooting the system.

Those parameters control how Linux kernel behaves, including things like:
- Networking settings
- Memory limits
- Process handling
- Security controls

Those parameters are stored in the /proc/sys/ directory.

If we change some parameters using the sysctl command, then those changes are not persistent across reboots.

If we want them to be consistent we need to create a .conf file in the /etc/sysctl.d/ folder and save those changes there.

For example this command:
- `sysctl -w net.ipv4.ip_forward=1`

changes the `net.ipv4.ip_forward` parameter which is stored in the /proc/sys/net/ipv4/ip_forward file.

If we want to have this parameter set up like this across reboots then we need to create a file like this:
- `echo “net.ipv4.ip_forward=1” > /etc/sysctl.d/filename.conf`