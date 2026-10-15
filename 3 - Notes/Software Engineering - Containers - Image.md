Tags: [[__DevOps]], [[__Infrastructure_Engineering]]

# Introduction
An image is a template used for running containers. 

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

#DevOps #DataEngineering 