Tags: [[__DevOps]], [[__Infrastructure_Engineering]]

# Introduction
A layer contains files which represents filesystem changes. A layer is a set of instructions for Docker about how to change an image’s filesystem.

Each instruction in a Dockerfile creates a layer.

If we want to add or modify a file in an image, then that file will appear in a layer.

If we want to remove a file from an image, then in a layer we will have a special whiteout file:
- .wh.filename

That tells Docker that this file needs to be removed from the filesystem in an image.

Those layers are applied one be one to create a final image. Each layer applies changes in the filesystem.

Each layer is saved on a computer.

For example if we have a Dockerfile like this:
```
COPY file1 /file1
RUN rm /file1
COPY file2 /file2
```

Then:
- The first layer will contain only a file1 (which we copied to the image from the host)
- The second layer will contain a whiteout file .wh.file1 which tells Docker that this file should be removed from the filesystem
- The third layer will contain only the file2

After building an image using this Dockerfile, Docker will apply each layer one by one and that will cause:
- Adding the file1 to the image
- Removing the file1 from the image
- Adding the file2 to the image
## Layers caching
Layers are cached. That means that if we build an image multiple times using the same Dockerfile, then we are gonna use saved layers from previous builds, if we didn’t change an instruction in the Dockerfile.
## Layers sharing
Layers can be shared across images. If we build mutliple images using the same base layer, for example containing Ubuntu, then we are not duplicating that layer. The same layer will be used for every image.

#DevOps #DataEngineering 