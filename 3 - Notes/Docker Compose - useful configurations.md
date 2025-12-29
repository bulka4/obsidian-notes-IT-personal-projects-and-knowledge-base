Tags: [[__DevOps]], [[__Infrastructure_Engineering]], [[_Docker]] 

# Run a command on container’s start

Below docker compose file will run a specified command when container starts (starts a bash session in this case):
![[2 - Images/Docker Compose - Useful configurations/Screenshot 1.png]]

# Get access to the container’s shell

Below docker compose file will allocate a pseudo TTY. It will make it possible to get access to the container’s shell from our terminal:
![[2 - Images/Docker Compose - Useful configurations/Screenshot 2.png]]

After we run such a container we can get access to its terminal by running this command:
```
docker exec -it <container -name> bash
```

# Map ports

We can specify how internal container’s ports are exposed to the host machine.

We specify it in a docker compose file like this:
```
ports:
	- "host_port:container_port"
```

So we specify which port on the host correspond to which host in a container.

This is needed if we want to connect to a process running in a container from outside of a container.

If we have a process running in a container listening on the port given by the container_port, and we want to connect to it from outside of the container, we can connect to it using localhost:host_port.

# Create a volume
![[2 - Images/Docker Compose - Useful configurations/Screenshot 3.png]]

# Mount a folder

We can mount a folder to a container so whenever we make change in this folder on the host, the same changes are reflected in the container.

It also works the other way around – changes made in the container are reflected on the host.
![[2 - Images/Docker Compose - Useful configurations/Screenshot 4.png]]

# Run container in a background

Docker compose up -d