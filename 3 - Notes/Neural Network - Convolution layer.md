Tags: [[__Machine_Learning]]

# Introduction
Convolution layer is one of types of layers in a neural network ([[Neural Network|link]]). Neural network containing a convolution layer is called a Convolutional Neural Network (CNN).

It is good for processing 2-D and 3-D data in general, for example:
- 2-D
	- Image - 2-D matrix where each element represents a color of a pixel.
	- Time series - For example audio or sensor measurements. For each timestep, we have measurements.
- 3-D
	- Image where each color is coded using a series of multiple numbers. For example RBG which encodes each color using 3 numbers.

More explanation about 2-D and 3-D inputs for models can be found here - [[Types of numeric inputs for ML models]].
## Patches, filters and feature map
Convolution layer partitions an input into smaller chunks called **patches** ([[Data patching|link]]), and **apply on them filters**.

For example, one patch can be such a part of a matrix:
$$
\text{patch} = \begin{pmatrix}
\colorbox{blue}{1} & \colorbox{blue}{2} & 3 \\
\colorbox{blue}{4} & \colorbox{blue}{5} & 6 \\
7 & 8 & 9 \\
\end{pmatrix}
 = \begin{pmatrix}
1 & 2 \\
4 & 5 \\
\end{pmatrix}
$$

By applying a filter we mean some specific calculations related to multiplying matrices, what is explained further in this document.

Applying a filter to a patch detect features in that patch, such as:
- Edges and other specific shapes in an image 
- Specific word in audio data
- Sensor measurements corresponding to some specific event (for example pressure measurements from a sensor on the floor corresponding to a person walking)

One filter detects one specific feature. We apply multiple filters, where each filter detects different features.

Output of a convolution layer is a set of matrices called **feature maps**. There is one feature map per filter. They contain features extracted from patches by filters. 

So output has a shape $(H, W, C)$, where $C$ is a number of filters applied. It can be seen as a matrix where each element is a vector of length $C$ which is a set of features extracted by different feature maps.
## Padding
Often, we use **padding** ([[Padding an input for a ML model|link]]) on the input for a convolution layer to enable better feature detection.
## Combining convolution layer with other types of layers
Output of a convolution layer (feature map) is often fed into a **pooling layer** ([[Neural Network - Pooling layer|link]]) to reduce its size and extract only the most important information.

Further, output of a convolution layer (or output of a pooling layer if used) is often fed into a dense layer ([[Neural Network - Fully-connected (dense) layer|link]]) to process extracted features and make predictions based on them. 
# Data input dimensions
Data input for a convolution layer are usually 2-D or 3-D tensors which represents for example an image or time series data with sensors measurements.

More information about those inputs with examples can be found here:
- 2-D tensor: [[Machine Learning models - 2-D input|link]]
- 3-D tensor: [[Machine Learning models - 3-D input|link]]
# Convolution layer
Convolution layer performs the following operations:
- Create a group of patches for an input $X$ 
- Apply a filter to each patch
- Save results of applying a filter for each patch in an output matrix $Y$

This process is explained in more detail in sections below.
## Patching
In a convolution layer, we perform data patching, that is a process where we prepare a group of patches (different parts of an input) and perform operations on them (applying a filter in this case).

To learn more about the core concepts, like what are:
- A patch
- Sliding a patch
- A stride
refer to this document - [[Data patching]].
## Applying a filter to patches to generate a feature map
A filter is a 3-D tensor $\large K \in \mathbb{R}^{k_h \times k_w \times C}$ .

Let's assume, that:
- The input for the convolution layer is a 3-D tensor $X \in \mathbb{R}^{H \times W \times C}$ 
- We prepared a group of patches $\large X_{\text{patch}[i, j]} \in \mathbb{R}^{k_h \times k_w \times C}$ 

We create a feature map $Y$ (a matrix), by applying the filter to different patches and saving results in the feature map $Y$.

Applying a filter to a patch, means multiplying them elementwise ([[Elementwise matrix multiplication|link]]) and taking a sum of all elements from the result of that multiplication.

So each element of $Y$ is defined as:
$$
\large
Y[i,j] = \sum_{i,j} a_{ij}, \quad \text{where } (a_{ij})_{k_w \times k_h} = X_{\text{patch}[i,j]} \odot K
$$
## Example (2-D input)
For example, if we have a 2-D input $X$ (matrix) and filter $K$ like that:
$$
X = \begin{pmatrix}
1 & 2 & 3 \\
4 & 5 & 6 \\
7 & 8 & 9 \\
\end{pmatrix}
, \quad K = \begin{pmatrix}
1 & 0 \\
0 & 1 \\
\end{pmatrix}
$$
and we use stride $(1, 1)$, then we receive patches like that:
$$
{\large X_{\text{patch}[1,1]} } = \begin{pmatrix}
\colorbox{blue}{1} & \colorbox{blue}{2} & 3 \\
\colorbox{blue}{4} & \colorbox{blue}{5} & 6 \\
7 & 8 & 9 \\
\end{pmatrix}
= \begin{pmatrix}
1 & 2 \\
4 & 5 \\
\end{pmatrix}
, \quad 
{\large X_{\text{patch}[1,2]} } = \begin{pmatrix}
1 & \colorbox{blue}{2} & \colorbox{blue}{3} \\
4 & \colorbox{blue}{5} & \colorbox{blue}{6} \\
7 & 8 & 9 \\
\end{pmatrix}
= \begin{pmatrix}
2 & 3 \\
5 & 6 \\
\end{pmatrix}
$$
$$
{\large X_{\text{patch}[2,1]} } = \begin{pmatrix}
1 & 2 & 3 \\
\colorbox{blue}{4} & \colorbox{blue}{5} & 6 \\
\colorbox{blue}{7} & \colorbox{blue}{8} & 9 \\
\end{pmatrix}
= \begin{pmatrix}
4 & 5 \\
7 & 8 \\
\end{pmatrix}
, \quad
{\large X_{\text{patch}[2,2]} } = \begin{pmatrix}
1 & 2 & 3 \\
4 & \colorbox{blue}{5} & \colorbox{blue}{6} \\
7 & \colorbox{blue}{8} & \colorbox{blue}{9} \\
\end{pmatrix}
= \begin{pmatrix}
5 & 6 \\
8 & 9 \\
\end{pmatrix}
$$
and for each patch we apply the filter, that is:
- Multiply the patch elementwise by the filter $K$ 
- Take a sum of all the elements from the result matrix
- Save results in $Y$ 

So in our example applying the filter looks like that: 
$$
\large
X_{\text{patch}[1,1]} \odot K = \begin{pmatrix}
1 \cdot 1 & 2 \cdot 0 \\
4 \cdot 0 & 5 \cdot 1 \\
\end{pmatrix}
= \begin{pmatrix}
1 & 0 \\
0 & 5 \\
\end{pmatrix}
\implies
Y[1,1] = 1 + 0 + 0 + 5 = 6
$$
$$
\large
X_{\text{patch}[1,2]} \odot K = \begin{pmatrix}
2 \cdot 1 & 3 \cdot 0 \\
5\cdot 0 & 6 \cdot 1 \\
\end{pmatrix}
= \begin{pmatrix}
2 & 0 \\
0 & 6 \\
\end{pmatrix}
\implies
Y[1,2] = 2 + 0 + 0 + 6 = 8
$$
$$
\large
X_{\text{patch}[2,1]} \odot K = \begin{pmatrix}
4 \cdot 1 & 5 \cdot 0 \\
7 \cdot 0 & 8 \cdot 1 \\
\end{pmatrix}
= \begin{pmatrix}
4 & 0 \\
0 & 8 \\
\end{pmatrix}
\implies
Y[2,1] = 4 + 0 + 0 + 8 = 12
$$

So a feature map is created by applying the filter to different patches:
![[Feature map.png]]
## Example (3-D input)
In case when $X$ is a 3-D tensor, then patches are also 3-D tensors, let's say of shape $(H, W, C)$. We can look at them as a set of $C$ matrices of shape $(H, W)$. So those are separate matrices per channel $C$.

For matrix for every channel $C$ we perform the same operation as in 2-D case from the previous example.

So for every channel $C$ we receive a number, and then we sum them up.
## Applying multiple filters
We can apply multiple filters where each one generates a matrix 
# Padding
Often, we also use a padding on the input before applying a convolution layer. More about padding can be found here - [[Padding an input for a ML model]].
## Why to use padding
Using padding causes that:
- An output has a bigger size
- Filter extracts features from the borders of $X$ better

Notice, how different patches we can select now near the borders of he padded $X$, for example:
$$
{\large X_{\text{patch}[i,j]} } = \begin{pmatrix}
\colorbox{blue}{0} & \colorbox{blue}{0} & 0 & 0 & 0 \\
\colorbox{blue}{0} & \colorbox{blue}{1} & 2 & 3 & 0 \\
0 & 4 & 5 & 6 & 0 \\
0 & 7 & 8 & 9 & 0 \\
0 & 0 & 0 & 0 & 0 \\
\end{pmatrix}
$$
And we have now more patches so output (feature map) will be bigger.
# Pooling
We can also use a pooling layer on the output of the convolution layer (feature map) to reduce its size and extract only the most important information from that feature map.

How pooling layer works is described here - [[Neural Network - Pooling layer]].
# Interpretation
Applying filter on a patch is supposed to detect features, such as:
- Edges and other specific shapes in an image 
- Specific word in audio data
- Sensor measurements corresponding to some specific event (for example pressure measurements from a sensor on the floor corresponding to a person walking)

That's why we select different patches, since those features might be present in different sections of the input.

Each filter produces a feature map, which is a collection of features extracted by this filter.

To show how filters detects features, let's take as an example a matrix representing an image:
$$
X = \begin{pmatrix}
10 & 13 & 200 \\
15 & 12 & 210 \\
12 & 8 & 205 \\
\end{pmatrix}
$$
where higher values means brighter color. So such an $X$ shows a vertical edge - it is bright on the left and dark on the right.

If we use the following filter:
$$
K = \begin{pmatrix}
-1 & 0 & 1 \\
-1 & 0 & 1 \\
-1 & 0 & 1 \\
\end{pmatrix}
$$
It will be detecting vertical edges. Let's calculate an output of applying this filter for our input $X$:
$$
X \odot K = \begin{pmatrix}
-10 & 0 & 200 \\
-15 & 0 & 210 \\
-12 & 0 & 205 \\
\end{pmatrix}
\implies
Y = (-10 + 0 + 200) + (-15 + 0 + 210) + (-12 + 0 + 205) = 578
$$
That is a high value which indicates that is a vertical edge. For an image without a vertical edge, that value would be much smaller.

Is there would be a vertical edge with a dark left side and bright right side, we would obtain $-578$ which is high negative number, also indicating the presence of a vertical edge.
# Convolution layer - Mathematical description
To see how to describe CNN mathematically, what variables do we have and calculations we perform, refer to this document - [[Neural Network - Convolution layer described mathematically]]

#MachineLearning 