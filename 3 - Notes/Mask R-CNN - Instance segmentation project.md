Tags: [[__My_projects]] [[__Machine_Learning]]
#MyProjects #MachineLearning 

# Introduction
In this project we have a code for a mask R-CNN model for instance segmentation, i.e. detecting objects in an image:
![[2 - Images/Mask R-CNN - Instance segmentation project/Screenshot 1.png]]

We also:
- Use a VGG tool for image annotation (creating bounding boxes and labels)
- Split a video into frames using a Python script
# Project code repository
A repository with a code for this project is here - [github.com](https://github.com/bulka4/mask_rcnn).
# Data
In this repository we have one video and a few images which we can use for testing:
- Splitting an image into frames
- Image annotation using the VGG tool
# Splitting video into frames
In the notebook, we have a code for splitting video into frames.
# VGG for image annotation
We use the VGG tool for image annotation - marking objects in images. It allows to create:
- Bounding boxes
- Labels

This repository and documentation doesn't help with how to install a VGG tool.
## Annotations file
The `example/annotations/example_json.json` file contains example annotations created for video frames using VGG.
# Model code
Model code is in:
- The `mrcnn_model` folder in this repository
- In this repository - [github.com](https://github.com/matterport/Mask_RCNN), in the `mcrnn` folder (it is the same code)
# Useful materials
- GitHub with the model - [github.com](https://github.com/matterport/Mask_RCNN) 
- Implementation on a different dataset (created by VGG tool): [github.com](https://github.com/michhar/pytorch-mask-rcnn-samples/blob/master/Train.ipynb) 
- Another github with FaceBook Detectron model: [github.com](https://github.com/facebookresearch/Detectron) 