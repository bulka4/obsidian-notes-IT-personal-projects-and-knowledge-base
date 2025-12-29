Tags: [[__DevOps]], [[__Infrastructure_Engineering]]

# Introduction
Dockerfile is a file which contains instructions which create an image.
## Instructions
### RUN
The RUN instruction is used in order to execute a command in container’s terminal.
### USER
We can use the USER instruction in order to change a user which will be executing a command used in the RUN instruction.
### SHELL
By default Docker run commands (from instructions like RUN, CMD, ENTRYPOINT) using sh (/bin/sh). Using the SHELL instruction we can change it. We can specify there which shell to use, for example this changes shell into bash:
```
SHELL ["/bin/bash", "-c"]
```
### COPY
Copy a file from a host to the created image. If has the following format:
```
COPY local_path container_path
```

Where:
- **Local_path** – Is a path on a local host where is located a file to copy. This path needs to be relative to the build context directory.
- **Container_path –** Is a path in a container where to save a file

**Options:**
- COPY file.txt /folder1/ – Copy the file file.txt to the folder folder1
- COPY file.txt /folder1/file_new.txt – Copy the file file.txt and save it in the container at the path /folder1/file_new.txt (rename the file)
- COPY folder1 /folder2/folder1 – Copy the folder folder1 to the container and save this folder at the path /folder2/folder1 (create a new folder)
### CMD
Specify what bash command will be executed when starting a container.
### ENTRYPOINT
Specify what bash script will be executed when starting a container.

#DevOps #DataEngineering 