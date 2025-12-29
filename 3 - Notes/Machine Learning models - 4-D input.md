Tags: [[__Machine_Learning]]

# Introduction
When input for a machine learning model is a 4-D tensor, that can be viewed as a series of 3-D tensors ([[Machine Learning models - 3-D input|link]]), for example 3-D tensors in different points in time.

Each 3-D tensor in that series, can be seen as a matrix where each element is a vector.

We usually denote its shape as $(T, H, W, C)$ which indicates:
- $T$ - Timestep
- $H$ - Input height
- $W$ - Input weight
- $C$ - Number of channels
# Examples
## Video
4-D tensor can represent a video, that is a series of 3-D tensors which represent images which change in time.

So we have:
- A 4-D tensor $\large x \in \mathbb{R}^{T \times H \times W \times C}$ which is a series of images
- For a a specific timestep $t$, we have a 3-D tensor $\large x_t \in \mathbb{R}^{H \times W \times C}$ which is an image

#MachineLearning 