Tags: [[__DevOps]], [[__Infrastructure_Engineering]]

# Introduction
We can mount a folder on host to a folder in a container. That means that all the files which we create in the host folder will be reflected in the container one and vice versa.

This is useful if we want to upload files to a container and have the same files even after restarting a container.

We can do it this way:
```
docker run <image-name> \
	-v host_path:container_path
```

**Folder permissions:**

If we run an app in a container, and that app wants to perform action (create, delete) on a file on the host which is mounted into the container, then user from the container which is running this app will be verified for permission.

The best practice is to create a user with a specific UID and GID in a container and grant permissions to the folder in container and on host for that UID and GID (just using a username is not enough, we need to use UID and GID when defining permissions).

If we create a user in a container without specifying UID and GID then those values are generated automatically. It is better to specify those values in that case so we know what are those values.

#DevOps #DataEngineering 