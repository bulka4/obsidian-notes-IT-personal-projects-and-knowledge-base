Tags: [[_Algebra]], [[__Mathematics]]

# Introduction
Vectorization of a matrix is operation which converts a matrix into a vector by stacking its columns:
$$
\begin{align}
& A = \begin{bmatrix}
a_{11} & \ldots & a_{1n} \\
\vdots &  & \vdots \\
a_{m1} & \ldots & a_{mn}
\end{bmatrix}
& \text{vec}(A) = \begin{bmatrix}
a_{11} \\
\vdots \\
a_{m1} \\
a_{12} \\
\vdots \\
a_{m2} \\
\vdots \\
a_{1n} \\
\vdots \\
a_{mn}
\end{bmatrix}
\end{align}
$$
# Mapping elements between matrices
We have the following mapping of elements between a matrix and its vectorized form:
$$
\large
\text{vec}(A)_j = A_{i,k}
$$
where:
- $\large k = \left\lfloor \frac{j - 1}{m} \right\rfloor + 1$ - A floor ([[Floor of a number|link]])
- $i = j - (k - 1)m$ 
# Properties
$$
\text{vec}(Wa) = (a^T \otimes I) \text{vec}(W)
$$
where $\otimes$ is Kronecker product ([[Kronecker product|link]]).

#Algebra #Mathematics 