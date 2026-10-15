Tags: [[__Software_Engineering]]
#SoftwareEngineering 

# Container vs VM
- VM virtualizes hardware - each VM gets assigned a separate hardware
- A container virtualizes the operating system environment - each container share the same hardware. They have only separate for example file system, network configs, environment variables.

More information can be found here - [[Software Engineering - Containers - Container vs VM]].
# Layer
- A layer contains files which represents filesystem changes. A layer is a set of instructions for the container runtime (e.g. Docker) about how to change an image’s filesystem.
- Each instruction in a Dockerfile creates a layer.
- If we want to add or modify a file in an image, then that file will appear in a layer.
- If we want to remove a file from an image, then in a layer we will have a special whiteout file: `.wh.filename`
	- That tells the container runtime that this file needs to be removed from the filesystem in an image.
- Those layers are applied one be one to create a final image. Each layer applies changes in the filesystem.

More information can be found here - [[Software Engineering - Containers - Layer]].
# Image
An image contains:
1. Layers ([[Software Engineering - Containers - Layer|link]])
	1. Each layer contains filesystem changes
	2. Layers are applied one by one which produces the final filesystem
2. Image configuration (not filesystem layers)
	- Environment variables defined with ENV
	- Instructions for starting processes, such as CMD and ENTRYPOINT

The filesystem produced by layers can contain:
1. OS/base filesystem layer
	- OS files (e.g., Ubuntu or Alpine filesystem)
	- System libraries and dependencies, if included in that layer
	  
	Note: a container image doesn't normally include its own kernel; containers use the host's kernel.
2. Other filesystem layers
	- Additional installed tools and packages
	- Application files
	- Other files added during the image build

More information can be found here - [[Software Engineering - Containers - Image]].
# Container
A container is a running instance of an image. In a container we have running processes specified in an image (started for example by a bash script specified in the CMD or ENTRYPOINT inscructions in a Dockerfile).

We can have multiple containers running using the same image.

Container adds additional writable layer to an image. If container modifies files it only affects the writable layer, not the image.

What a container and a host machine have separate:
- Filesystem (including Operating System files)
- Processes

What they have common:
- Kernel ([[Operating systems - Kernel|link]])

More information can be found here - [[Software Engineering - Containers - Container]].
# Dockerfile
Dockerfile is a file which contains instructions which create an image.

More information can be found here - [[Software Engineering - Containers - Dockerfile]].
# Bind mounting volumes
- We can mount a folder on host to a folder in a container. That means that all the files which we create in the host folder will be reflected in the container one and vice versa.
- This is useful if we want to upload files to a container and have the same files even after restarting a container.
- all the data saved in the container’s folder at a given path will be saved on the host and available in the container after rerunning it.

More information can be found here - [[Software Engineering - Containers - Bind mounting volumes]]
# Other topics
1. [[Software Engineering - Containers - Build context directory]]
2. [[Software Engineering - Containers - OCI standard]]
3. [[Software Engineering - Containers - Union filesystem]]
4. [[Software Engineering - Containers - Network namespace]]
5. [[Software Engineering - Containers - Network drivers]]
	- [[Software Engineering - Containers - Network drivers - Bridge network]]
	- [[Software Engineering - Containers - Network drivers - Host network]]
	- [[Software Engineering - Containers - Network drivers - None network]]
	- [[Software Engineering - Containers - Network drivers - Overlay network]]
6. [[Software Engineering - Containers - Security]]
		- [[Software Engineering - Containers - Security - Root inside container]]
		- [[Software Engineering - Containers - Security - Linux capabilities]]
		- [[Software Engineering - Containers - Security - Dropping privileges]]
		- [[Software Engineering - Containers - Security - Read-only filesystem]]
		- [[Software Engineering - Containers - Security - Image scanning]]
		- [[Software Engineering - Containers - Security - Secrets handling]]
# Related topics
1. [[Software Engineering - Containers - Container vs VM]]
2. [[Software Engineering - Containers - Image]]
3. [[Software Engineering - Containers - Container]]
4. [[Software Engineering - Containers - Layer]]
5. [[Software Engineering - Containers - Dockerfile]]
6. [[Software Engineering - Containers - Build context directory]]
7. [[Software Engineering - Containers - Bind mounting volumes]]
8. [[Software Engineering - Containers - OCI standard]]
9. [[Software Engineering - Containers - Union filesystem]]
10. [[Software Engineering - Containers - Network namespace]]
11. [[Software Engineering - Containers - Network drivers]]
	- [[Software Engineering - Containers - Network drivers - Bridge network]]
	- [[Software Engineering - Containers - Network drivers - Host network]]
	- [[Software Engineering - Containers - Network drivers - None network]]
	- [[Software Engineering - Containers - Network drivers - Overlay network]]
12. [[Software Engineering - Containers - Security]]
	- [[Software Engineering - Containers - Security - Root inside container]]
	- [[Software Engineering - Containers - Security - Linux capabilities]]
	- [[Software Engineering - Containers - Security - Dropping privileges]]
	- [[Software Engineering - Containers - Security - Read-only filesystem]]
	- [[Software Engineering - Containers - Security - Image scanning]]
	- [[Software Engineering - Containers - Security - Secrets handling]]