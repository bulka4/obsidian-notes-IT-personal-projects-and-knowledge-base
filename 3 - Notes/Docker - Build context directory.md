Tags: [[__DevOps]], [[__Infrastructure_Engineering]]

# Introduction
Build context directory is a directory which contains the Dockerfile and all the other files which will be used in the Dockerfile (which we will copy into an image using the COPY or ADD instructions).

We provide a path to this directory in the ‘docker build’ command.

What path we will need to specify in the COPY instruction depends on this path.

#DevOps #DataEngineering 