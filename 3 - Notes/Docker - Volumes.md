Tags: [[__DevOps]], [[__Infrastructure_Engineering]]

# Introduction
We can use volumes so we don’t loose data after rerunning a container.

After creating a volume, data saved in a specific container’s folder will be saved on the host.

We create volume this way:
```
docker run <image-name> \
	-v volume_name:container_path
```

Then all the data saved in the container’s folder at the path given by the container_path, will be saved on the host and available in the container after rerunning it.

#DevOps #DataEngineering 