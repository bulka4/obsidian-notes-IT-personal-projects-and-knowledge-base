Tags: [[__DevOps]], [[__Infrastructure_Engineering]]

# Introduction
A container is a running instance of an image. In a container we have running processes specified in an image (started for example by a bash script specified in the CMD or ENTRYPOINT inscructions in a Dockerfile).

 We can have multiple containers running using the same image.

Container adds additional writable layer to an image. If container modifies files it only affects the writable layer, not the image.

What a container and a host machine have separate:
- Filesystem (including Operating System files)
- Processes

What they have common:
- Kernel ([[Operating systems - Kernel|link]])

#DevOps #DataEngineering 