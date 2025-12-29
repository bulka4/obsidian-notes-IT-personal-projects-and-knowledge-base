Tags: [[__Machine_Learning]]

# Introduction
Data patching is a technique where we select different parts (called patches) of an input, which is either a 2-D or 3-D tensor ([[Types of numeric inputs for ML models|link]]), and then perform some operation on each patch.

For example, a patch might be a fragment of an image.

It is used commonly in neural networks ([[Neural Network|link]]), for example in a pooling layer, where from each patch we select max or average value, or in a convolution layer, where we multiply patch by another matrix called filter.
# What is a patch
For a 3-D input tensor $X \in \mathbb{R}^{H \times W \times C}$, patch is its part of a shape:
$$
\large
X_{\text{patch}[i,j]} \in \mathbb{R}^{H_p \times W_p \times C}
$$
where $H_p < H,\ W_p < W$. Number of channels (the third dimension $C$) stays the same.

We can create different patches, containing different parts of $X$, that's why we use $[i,j]$ indexes to distinguish different patches.
# How to create patches
## The first patch
To create the first patch $\large X_{\text{patch}[1,1]}$, we select a part of the input tensor $X$ which is in the top left-hand corner of $X$, and which has a shape $(H_p, W_p, C)$ .

For example:
$$
\large
X = \begin{pmatrix}
x_{11} & x_{12} & x_{13} \\
x_{21} & x_{22} & x_{23} \\
x_{31} & x_{32} & x_{33} \\
\end{pmatrix}
, \quad
X_{\text{patch}[1,1]} = \begin{pmatrix}
\colorbox{blue}{$x_{11}$} & \colorbox{blue}{$x_{12}$} & x_{13} \\
\colorbox{blue}{$x_{21}$} & \colorbox{blue}{$x_{22}$} & x_{23} \\
x_{31} & x_{32} & x_{33} \\
\end{pmatrix}
$$
so in that case, shapes of $X$ and $X_{\text{patch}[1,1]}$ are:
- $H = W = 3$ 
- $H_p = W_p = 2$. 

and elements $x_{ij} = [x_{ij}[1], \ldots, x_{ij}[C]]$ are vectors of length $C$ (number of channels). If $C=1$, then those are normal numbers.

This way we create our first patch noted as $\large X_{\text{patch}[1,1]}$ .
## Sliding the patch and Stride
To create further patches, we will slide the previous patch to the right, in the same row, by a specified number of columns.

When we reach the end of a row, we will slide the patch down by a specified number for rows, to the beginning of a new row.

A **stride** is a pair $(s_h, s_w)$ which specifies, by how many rows and columns we slide the patch at each step:
- $s_h$ - Number of rows to slide the patch down
- $s_w$ - Number of columns to slide the patch to the right

For example, for a stride $(1, 1)$, we will receive further patches like that:
$$
X_{\text{patch}[1,2]} = \begin{pmatrix}
x_{11} & \colorbox{blue}{$x_{12}$} & \colorbox{blue}{$x_{13}$} \\
x_{21} & \colorbox{blue}{$x_{22}$} & \colorbox{blue}{$x_{23}$} \\
x_{31} & x_{32} & x_{33} \\
\end{pmatrix}
, \quad
X_{\text{patch}[2,1]} = \begin{pmatrix}
x_{11} & x_{12} & x_{13} \\
\colorbox{blue}{$x_{21}$} & \colorbox{blue}{$x_{22}$} & x_{23} \\
\colorbox{blue}{$x_{31}$} & \colorbox{blue}{$x_{32}$} & x_{33} \\
\end{pmatrix}
$$
## When to stop
We stop sliding the patch, when we are near the end of the final row, such that if we slide the patch further, we will end up outside of the input $X$ .

For example, if we have a patch like that:
$$
X_{\text{patch}[1,2]} = \begin{pmatrix}
x_{11} & \colorbox{blue}{$x_{12}$} & \colorbox{blue}{$x_{13}$} \\
x_{21} & \colorbox{blue}{$x_{22}$} & \colorbox{blue}{$x_{23}$} \\
x_{31} & x_{32} & x_{33} \\
\end{pmatrix}
$$
and stride $(2, 1)$, then we can't progress because moving we can't move that patch 2 rows below.
## Patch indexes
We use indexes $[i,j]$ to distinguish different patches and to indicate which regions of $X$ they are equal to:
$$
\large X_{\text{patch}[i,j]} = X[i \cdot s_w : i \cdot s_w + W_p,\ 
j \cdot s_h : j \cdot s_h + H_p,\ :]
$$

Note, that we select here values for all the channels (all values from the third dimension).

In short, we could say that $\large X_{\text{patch}[i,j]}$ corresponds to the $i$-th row and $j$-th column but that is not precise. The above formula tells us precisely what region of $X$ the patch equals to.

Mapping the other way, that for a given element $x_{ij} \in X$ to find coordinates of the same element in all the patches which contain it, is possible but very tricky to do, and usually we don't need that, so we will not be covering that here in this document.
## Performing operations on patches
We select patches to perform some operations on them and save the result of each patch in another matrix.

For example, in a pooling neural network layer ([[Neural Network - Pooling layer|link]]), we select a max or average from each patch, or in a convolution neural network layer ([[Neural Network - Convolution layer|link]]) we multiply that patch by another matrix called filter.

Result of performing that operation on the patch $\large X_{\text{patch}[i,j]}$ is saved in the output matrix in the $i$-th row and $j$-th column - $Y[i, j]$.

#MachineLearning 