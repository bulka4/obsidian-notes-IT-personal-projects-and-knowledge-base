Tags: [[__DevOps]], [[__Infrastructure_Engineering]], [[_Docker]] 

# Build an image

When we build an image we need to either run the ‘docker build’ command from a folder which contains a Dockerfile and all the other files needed or use this command:

· Docker build -f docker_file_path -t image_name build-context-directory-path

Note:

· Build context directory is a directory which contains the Dockerfile and all the other files which will be used in the Dockerfile (which we will copy into an image using the COPY or ADD instructions).

Where:

· **docker_file_path** - A path to the Dockerfile which will be used for building an image. We don’t need to provide it if the Dockerfile is called ‘Dockerfile’ and it is located in the build context directory.

· **build-context-directory-path** – A path to the build context directory.

Additional options:

· --no-cache – don’t use caching

When we run for example ‘COPY’ instruction in the Dockerfile then we need to provide there

# Get access to a container’s shell

## Get access to a running container’s shell

Docker exec runs a new command inside of a running container. For example if we run:
```
Docker exec -it <container_name_or_id> /bin/bash
```

it allocates a pseudo terminal and gives us access to the container’s shell from our terminal.

## Run a container and get immediately access to its shell
```
docker run -it <image-name> /bin/bash
```
# Removing

## containers

Remove one container: 
```
docker rm <container-ID-or-name>
```
Remove all containers: 
```
docker rm $(docker ps -aq)
```
If containers are running, we need to stop them first using ‘docker stop’:
```
Docker stop <container-id-or-name> # stop a specific container
docker stop $(docker ps -aq) # stop all the containers
```
## images

Remove one image: 
```
docker rmi <image-name-or-ID>
```
Remove all the images: 
```
docker rmi $(docker image ls -aq)
```
Remove dangling images (untagged build cache layers):
```
docker image prune
```
Remove all unused images (untagged build cache layers):
```
docker image prune -a
```
Remove dangling build cache:
```
docker builder prune
```
Remove all build cache:
```
docker builder prune --all
```
## volumes
Delete all the volumes:
```
docker volume rm $(docker volume ls -q)
```
## netwoks (except for the default one)
```
docker network rm $(docker network ls -q)
```
## build cache
```
docker builder prune -a
```
## everything
```
docker system prune --all --volumes
```
# Run container in a background
```
Docker run <image-name> -d
```
