Tags: [[__Infrastructure_Engineering]] [[_Linux & Bash]]
#InfrastructureEngineering #LinuxBash 

# Chmod
Chmod is changing permissions for a specific file or folder. It uses this syntax:
- `chmod xxx file_path`

Where xxx are numbers specifying the permissions.
# Chown
Chown is changing an owner of a file or folder. It uses this syntax:
- `chown [options] [username][:usergroup] file_path`

Where:
- `Username` – username of a new owner
- `:usergroup` (optional) a new group owner

Popular options:
- -R – change ownership of all the files and folders which are contained in the folder given by the file_path parameter.