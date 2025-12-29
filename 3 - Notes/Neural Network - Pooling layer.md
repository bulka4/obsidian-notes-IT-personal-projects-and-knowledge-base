Tags: [[__Machine_Learning]]

# Introduction
Pooling is a type of a neural network layer ([[Neural Network|link]]) used to reduce size of a tensor. It selects different patches (parts of an input tensor) (like described here - [[Data patching|link]]) and converts them into a single number to reduce size of the input.

There are different types of a pooling layer, which perform different operations in order to convert a patch into a single number:
- Max - Select a max number from the patch
- Average - Select an average from the patch

For a 3-D input tensor $X \in \mathbb{R}^{H \times W \times C}$, output of a pooling layer is also a 3-D tensor ([[Types of numeric inputs for ML models|link]]) $\large Y \in \mathbb{R}^{H_p \times W_p \times C}$, where:
- $H_p < H$
- $W_p < W$ 
- $Y[i, j]$ corresponds to the patch $\large X_{\text{patch}[i,j]}$ 

Number of channels (value $C$ in the third dimension) stays the same.
# How it works
For example, let's take as an input a 3-D tensor $X \in \mathbb{R}^{H \times W \times C}$ like this:
$$
\large
X = \begin{pmatrix}
x_{11} & x_{12} & x_{13} \\
x_{21} & x_{22} & x_{23} \\
x_{31} & x_{32} & x_{33} \\
\end{pmatrix}
$$
where elements $x_{ij} = [x_{ij}[1], \ldots, x_{ij}[C]]$ are vectors of length $C$ (number of channels).

We select different patches:
$$
{\large X_{\text{patch}[1,1]} } = \begin{pmatrix}
\colorbox{blue}{$x_{11}$} & \colorbox{blue}{$x_{12}$} & x_{13} \\
\colorbox{blue}{$x_{21}$} & \colorbox{blue}{$x_{22}$} & x_{23} \\
x_{31} & x_{32} & x_{33} \\
\end{pmatrix}
= \begin{pmatrix}
x_{11} & x_{12}\\
x_{21} & x_{22}\\
\end{pmatrix}
, \quad 
{\large X_{\text{patch}[1,2]} } = \begin{pmatrix}
x_{11} & \colorbox{blue}{$x_{12}$} & \colorbox{blue}{$x_{13}$} \\
x_{21} & \colorbox{blue}{$x_{22}$} & \colorbox{blue}{$x_{23}$} \\
x_{31} & x_{32} & x_{33} \\
\end{pmatrix}
= \begin{pmatrix}
x_{12} & x_{13}\\
x_{22} & x_{23}\\
\end{pmatrix}
$$
$$
{\large X_{\text{patch}[2,1]} } = \begin{pmatrix}
x_{11} & x_{12} & x_{13} \\
\colorbox{blue}{$x_{21}$} & \colorbox{blue}{$x_{22}$} & x_{23} \\
\colorbox{blue}{$x_{31}$} & \colorbox{blue}{$x_{32}$} & x_{33} \\
\end{pmatrix}
= \begin{pmatrix}
x_{21} & x_{22}\\
x_{31} & x_{32}\\
\end{pmatrix}
, \quad
{\large X_{\text{patch}[2,2]} } = \begin{pmatrix}
x_{11} & x_{12} & x_{13} \\
x_{21} & \colorbox{blue}{$x_{22}$} & \colorbox{blue}{$x_{23}$} \\
x_{31} & \colorbox{blue}{$x_{32}$} & \colorbox{blue}{$x_{33}$} \\
\end{pmatrix}
= \begin{pmatrix}
x_{22} & x_{23}\\
x_{32} & x_{33}\\
\end{pmatrix}
$$

and for each patch, we select a maximum or average. So an output of a pooling layer is a matrix:
$$
\large
\text{pool}(X) = \begin{pmatrix}
\max(X_{\text{patch}[1,1]}) & \max(X_{\text{patch}[1,2]}) \\
\max(X_{\text{patch}[2,1]}) & \max(X_{\text{patch}[2,2]}) \\
\end{pmatrix}
$$

#MachineLearning 