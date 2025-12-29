Tags: [[__Machine_Learning]]

# Introduction
This document describes a convolution layer mathematically, what variables do we have and what calculations we perform.

Before reading this, it is worth to read the introduction here - [[Neural Network - Convolution layer]], to see on a high level how convolution layer works and get the intuition.
# Data input
Data input is:
$$
\large
X \in \mathbb{R}^{H_{\text{in}} \times W_{\text{in}} \times C_{\text{in}}}
$$
where:
- $H_{\text{in}}$ - Input height
- $W_{\text{in}}$ - Input width
- $C_{\text{in}}$ - Number of input channels
## Padding
Let's use padding $(p_h, p_w)$ and denote padded $X$ as:
$$
\large X_{\text{pad}} \in \mathbb{R}^{(H_{\text{in}} + 2p_h) \times (W_{\text{in}} + 2 p_w) \times C_{\text{in}}} = \mathbb{R}^{H_{\text{pad}} \times W_{\text{pad}} \times C_{\text{in}}}
$$
To learn more about padding, refer to this document - [[Padding an input for a ML model]].
## Patching
We will prepare a group of patches to which we will be applying a filter to create a feature map, like explained in the introduction - [[Neural Network - Convolution layer]].
### Patch
Let's denote a patch of a padded input $X_{\text{pad}}$ as:
$$
\large X_{\text{patch}[i, j]} \in \mathbb{R}^{k_h \times k_w \times C_{\text{in}}}
$$
which looks like this:
$$
\large
X_{\text{patch}[i, j]} = X_{\text{pad}}[
	i \cdot s_h : i \cdot s_h + k_h
	,\ j \cdot s_w : j \cdot s_w + k_w
	,\ 1 : C_{in}]
$$

Shape of a patch needs to be the same as shape of the filter's weight $K^{(m)}$ which we define later in this document.

Relation between elements in $\large X_{\text{patch}[i, j]}$ and $\large X_{\text{pad}}$ is:
$$
\large X_{\text{patch}[i, j]} [r, c, C] = X_{\text{pad}} [
i \cdot s_h + r,\ j \cdot s_w + c,\ C]
$$

A given element $\large X_{\text{pad}} [r, c, C]$, can appear in multiple patches $\large X_{\text{patch}[i,j]}$. It would be possible to find all the patches which contains given element of $X_{\text{pad}}$ and their locations, but it is difficult and not necessary to build a convolution layer.
### Stride
We define stride as a pair $(s_h, s_w)$ which means that:
- Each time we slide a patch for a given row, we slide it by $s_w$ columns
- When we slide a patch to the next row, we slide it by $s_h$ rows
# Convolution operation
## Filters (parameters)
We have $C_{\text{out}}$ filters (kernels) which are learnable parameters. Each filter consist of a 3-D tensor:
$$
\large
K^{(m)} \in \mathbb{R}^{k_h \times k_w \times C_{\text{in}}}
$$
and bias:
$$
b^{(m)} \in \mathbb{R}
$$
for $m = 1, \ldots, C_{out}$.

Shape of the filter's weight $K^{(m)}$ needs to be the same as shape of a patch $X_{\text{patch}[i,j]}$ which we defined earlier.
## Calculating output
For a given:
- Stride $(s_h, s_w)$ 
- Padding $(p_h, p_w)$ 
- Set of filters $K^{(m)}, b^{(m)}$ 

an output tensor is:
$$
\large
Y \in \mathbb{R}^{H_{\text{out}} \times W_{\text{out}} \times C_{\text{out}}}
$$
where:
$$
H_{\text{out}} = \left\lfloor \frac{H_{\text{in}} - k_h + 2p_h}{s_h} \right\rfloor + 1
, \quad W_{\text{out}} = \left\lfloor \frac{W_{\text{in}} - k_w + 2p_w}{s_w} \right\rfloor + 1
$$
and each element of $Y$ is defined as:
$$
\large
Y[i,\ j,\ m] = b^{(m)} + \sum_{c=1}^{C_{\text{in}}} \sum_{u=1}^{k_{h}} \sum_{v=1}^{k_{w}}
X_{\text{pad}}[i \cdot s_h + u - 1,\ j \cdot s_w + v - 1,\ c]
K^{(m)}[u,\ v,\ c]
$$
## Vectorized form
Let's flatten both the patch and filter:
$$
\large
\begin{align}
& x_{ij} \in \mathbb{R}^{k_h k_w C_{\text{in}}} \text{ - flattened } 
X_{\text{patch}[i, j]} \\
& k^{(m)} \in \mathbb{R}^{k_h k_w C_{\text{in}}} \text{ - flattened } 
K^{(m)} \\
\end{align}
$$
Then we can write $Y$ as:
$$
Y[i, j, m] = x^T_{i,j} k^{(m)} + b^{(m)}
$$
where $\text{vec}()$ is a matrix vectorization ([[Vectorization of a matrix|link]]).

This equation is used in practice to program calculating the output $Y$.

In the section below we describe how variables from that equation look like.
### How variables look like
Here we will describe how variables from the above equation look like:
$$
Y[i, j, m] = x^T_{i,j} k^{(m)} + b^{(m)}
$$
We can look at 3-D variables:
- $\large X_{\text{patch}[i,j]} \in \mathbb{R}^{k_h \times k_w \times C_{\text{in}}}$ 
- $\large K^{(m)} \in \mathbb{R}^{k_h \times k_w \times C_{\text{in}}}$ 
as sets of matrices for different channels $C_{\text{in}}, C_{\text{out}}$. 

Let's denote matrices for a given channel $C_{i}$ as:
- $\large X_{\text{patch}[i,j]}^{C_i} \in \mathbb{R}^{k_h \times k_w}$ 
- $\large K^{(m)}_{C_i} \in \mathbb{R}^{k_h \times k_w}$ 

also let's denote the entire column $i$ of a matrix as:
$$
A[:, i], \quad A \text{ - matrix}
$$
then, our variables are stacked columns of matrices for different channels and they look like that:
$$
\large
x_{ij} = \begin{pmatrix}
X_{\text{patch}[i,j]}^{C_1}[:, 1] \\
\vdots \\
X_{\text{patch}[i,j]}^{C_1}[:, k_w] \\
X_{\text{patch}[i,j]}^{C_2}[:, 1] \\
\vdots \\
X_{\text{patch}[i,j]}^{C_{in}}[:, 1] \\
\vdots \\
X_{\text{patch}[i,j]}^{C_{in}}[:, k_w] \\
\end{pmatrix}
, \quad
k^{(m)} = \begin{pmatrix}
K^{(m)}_{C_1}[:, 1] \\
\vdots \\
K^{(m)}_{C_1}[:, k_w] \\
K^{(m)}_{C_2}[:, 1] \\
\vdots \\
K^{(m)}_{C_{\text{in}}}[:, 1] \\
\vdots \\
K^{(m)}_{C_{\text{in}}}[:, k_w] \\
\end{pmatrix}
,\quad
b^{(m)} \in \mathbb{R}
$$
So those are matrices of the following format:
$$
x_{ij} = \begin{pmatrix}
\text{Column 1, channel 1 of } X_{\text{patch}[i,j]} \\
\vdots \\
\text{Column } k_W \text{, channel 1 of } X_{\text{patch}[i,j]} \\
\text{Column 1, channel 2 of } X_{\text{patch}[i,j]} \\
\vdots \\
\text{Column 1, channel } C_{\text{in}} \text{ of } X_{\text{patch}[i,j]} \\
\vdots \\
\text{Column } k_w \text{, channel } C_{\text{in}} \text{ of } X_{\text{patch}[i,j]} \\
\end{pmatrix}
, \quad
k^{(m)} = \begin{pmatrix}
\text{Column 1, channel 1 of } K^{(m)} \\
\vdots \\
\text{Column } k_W \text{, channel 1 of } K^{(m)} \\
\text{Column 1, channel 2 of } X_{\text{patch}[i,j]} \\
\vdots \\
\text{Column 1, channel } C_{\text{in}} \text{ of } K^{(m)} \\
\vdots \\
\text{Column } k_w \text{, channel } C_{\text{in}} \text{ of } K^{(m)} \\
\end{pmatrix}
$$
### How to find a specific element in a vectorized form
To find a specific element in a vectorized forms of:
- Patch $\large X_{\text{patch}[i,j]}$ 
- Filter $K^{(m)}$ 

We can use those formulas:
$$
\large X_{\text{patch}[i,j]} [r, c, C] = x_{ij} [
C \cdot (k_h k_w) + c \cdot k_h + r]
$$
$$
\large K^{(m)}[r, c, C] = k^{(m)} [
C \cdot (k_h k_w) + c \cdot k_h + r]
$$
## Additional conceptual formula
It is also possible to write the following formula:
$$
\text{vec}(Y) = W \text{vec}(X_{\text{pad}}) + b
$$
which shows, that convolution is a linear operation.

But it is not used in practice to create a convolution layer, the previous formula from the 'Vectorized form' section is simpler to implement and it is enough.

Sections below explain how variables from the above equation look like.
### How variables look like
Here we will describe how variables from the above equations look like:
$$
\text{vec}(Y) = W \text{vec}(X_{\text{pad}}) + b
$$

We can look at 3-D variables:
- $\large X_{\text{pad}} \in \mathbb{R}^{(H_{\text{in}} + 2p_h) \times (W_{\text{in}} + 2 p_w) \times C_{\text{in}}} = \mathbb{R}^{H_{\text{pad}} \times W_{\text{pad}} \times C_{\text{in}}}$
- $\large Y \in \mathbb{R}^{H_{\text{out}} \times W_{\text{out}} \times C_{\text{out}}}$ 
as sets of matrices for different channels $C_{\text{in}}, C_{\text{out}}$. 

Let's denote matrices for a given channel $C_{i}$ as:
- $\large X_{\text{pad}}^{C_{i}} \in \mathbb{R}^{(H_{\text{in}} + 2p_h) \times (W_{\text{in}} + 2 p_w)} = \mathbb{R}^{H_{\text{pad}} \times W_{\text{pad}}}$ 
- $\large Y^{C_i} \in \mathbb{R}^{H_{\text{out}} \times W_{\text{out}}}$ 

also let's denote the entire column $i$ of a matrix as:
$$
A[:, i], \quad A \text{ - matrix}
$$
then, our variables are stacked columns of matrices for different channels and they look like that:
$$
\large
\text{vec}(Y) = \begin{pmatrix}
Y^{C_1}[:, 1] \\
\vdots \\
Y^{C_1}[:, W_{\text{out}}] \\
Y^{C_2}[:, 1] \\
\vdots \\
Y^{C_{\text{out}}}[:, 1] \\
\vdots \\
Y^{C_{\text{out}}}[:, W_{\text{out}}] \\
\end{pmatrix}
, \quad
\text{vec}(X_{\text{pad}}) = \begin{pmatrix}
X_{\text{pad}}^{C_1}[:, 1] \\
\vdots \\
X_{\text{pad}}^{C_1}[:, W_{\text{pad}}] \\
X_{\text{pad}}^{C_2}[:, 1] \\
\vdots \\
X_{\text{pad}}^{C_{\text{in}}}[:, 1] \\
\vdots \\
X_{\text{pad}}^{C_{\text{in}}}[:, W_{\text{pad}}] \\
\end{pmatrix}
$$
### How to find a specific element in a vectorized form
To find a specific element in a vectorized forms of:
- Padded input $X_{\text{pad}}$ 
- Output $Y$ 

We can use those formulas:
$$
\large X_{\text{pad}}[r, c, C] = \text{vec}(X_{\text{pad}}) [
C \cdot (H_{\text{pad}} W_{\text{pad}}) + c \cdot H_{\text{pad}} + r]
$$
$$
\large Y[r, c, C] = \text{vec}(Y) [
C \cdot (H_{\text{out}} W_{\text{out}}) + c \cdot H_{\text{out}} + r]
$$
### How W looks like
Variable $W$ is slightly different. It has the following shape:
$$
\Large
W \in \mathbb{R}^{(H_{\text{out}} W_{\text{out}} C_{\text{out}})
\times (H_{\text{pad}} W_{\text{pad}} C_{\text{in}})}
$$
It is possible but very difficult to calculate the exact values of elements of $W$. It is not necessary to create and use convolution layer, so we will skip this. We will just explain on a high level how $W$ looks like.

The $m$-th row of $W$:
- Will be multiplied by a column of $\text{vec}(X_{\text{pad}})$
- Corresponds to one output element $Y[i, j, m]$, that is one row of $\text{vec}(Y)$ for some $i, j$ 
- Contains values of the flattened filter $k^{(m)}$ 
- Values of $k^{(m)}$ are placed in columns in a row, which corresponds to the elements of a single patch $\large X_{\text{patch}[i,j]}$ for some $i, j$ 
- All other values are zeros

So the $m$-th row of $W$ is:
$$
\large
W_{m, :} = [w_{m C_1}, \ldots, w_{m C_{\text{in}}}, ]
$$
where each $\Large w_{m C_i}$ corresponds to the channel $C_i$ and it is another vector:
$$
\large
w_{m C_i} = [w_{m C_i 1}, \ldots, w_{m C_i W_{\text{pad}}}]
$$
where each $\Large w_{m C_i j}$ corresponds to:
- The channel $C_i$ 
- $j$-th column of $\large X_{\text{pad}}^{C_i}$
and it is another vector:
$$
\large
\large w_{m C_i j} = [w_{m C_i j 1}, \ldots, w_{m C_i j H_{\text{pad}}}]
$$
where each $\Large w_{m C_i j l}$ corresponds to:
- The channel $C_i$ 
- $j$-th column of $\large X_{\text{pad}}^{C_i}$
- $l$-th row of the $j$-th column of $\large X_{\text{pad}}^{C_i}$

So:
$$
\large
\begin{align}
& W_{m, :} = [\underbrace{
w_{m C_1 1 1}, \ldots, w_{m C_1 1 H_{\text{pad}}}}_{
\text{channel 1, column 1 of } X_{\text{pad}}}, 
\underbrace{
w_{m C_1 2 1}, \ldots, w_{m C_1 2 H_{\text{pad}}}}_{
\text{channel 1, column 2 of } X_{\text{pad}}}, \ldots, 
\underbrace{
w_{m C_1 W_{\text{pad}} 1}, \ldots, w_{m C_1 W_{\text{pad}} H_{\text{pad}}}}_{
\text{channel 1, column } W_{\text{pad}} \text{ of } X_{\text{pad}}}, \ldots \\
& \qquad \qquad \ldots \\
& \qquad \qquad 
\underbrace{
w_{m C_{\text{in}} 1 1}, \ldots, w_{m C_{\text{in}} 1 H_{\text{pad}}}}_{
\text{channel } C_{\text{in}} \text{, column 1 of} X_{\text{pad}}}, 
\underbrace{
w_{m C_{\text{in}} 2 1}, \ldots, w_{m C_{\text{in}} 2 H_{\text{pad}}}}_{
\text{channel } C_{\text{in}} \text{, column 2 of} X_{\text{pad}}}, \ldots, 
\underbrace{
w_{m C_{\text{in}} W_{\text{pad}} 1}, \ldots, w_{m C_{\text{in}} W_{\text{pad}} H_{\text{pad}}}}_{
\text{channel } C_{\text{in}} \text{, column } W_{\text{pad}} \text{ of } X_{\text{pad}}} \\
& \qquad \qquad ]

\end{align}
$$
Each element $\Large w_{m C_i j l}$ is a filter value which correspond to the element of $X_{\text{pad}}$:
$$
\Large w_{m C_i j l} \rightarrow X_{\text{pad}}[l,\ j,\ C_i]
$$
# Questions
- what is cross-correlation?
- 

#MachineLearning 