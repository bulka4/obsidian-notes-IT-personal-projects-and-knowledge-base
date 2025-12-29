Tags: [[_Algebra]], [[__Mathematics]]

# Introduction
Kronecker product for matrices $\large A = \{a_{ij}\}_{m \times n}$, $\large B = \{b_{ij}\}_{p \times q}$ is defined as:
$$
\large
A \otimes B = \begin{bmatrix}
a_{11}B &  \ldots &  a_{1n}B \\
\vdots & & \vdots \\
a_{m1}B &  \ldots &  a_{mn}B \\
\end{bmatrix}
=
\begin{bmatrix}
a_{11}b_{11} &  \ldots &  a_{11}b_{1q} 
& \ldots & a_{1n}b_{11} &  \ldots &  a_{1n}b_{1q} \\
\vdots & & \vdots \\
a_{11}b_{p1} &  \ldots &  a_{11}b_{pq} 
& \ldots & a_{1n}b_{p1} &  \ldots &  a_{1n}b_{pq} \\
\vdots & & \vdots & & \vdots & & \vdots \\
a_{m1}b_{11} &  \ldots &  a_{m1}b_{1q} 
& \ldots & a_{mn}b_{11} &  \ldots &  a_{mn}b_{1q} \\
\vdots & & \vdots \\
a_{m1}b_{p1} &  \ldots &  a_{m1}b_{pq} 
& \ldots & a_{mn}b_{p1} &  \ldots &  a_{mn}b_{pq} \\
\end{bmatrix}
$$
# Properties
$$
\text{vec}(Wa) = (a^T \otimes I) \text{vec}(W)
$$
where vec() is vectorization of a matrix ([[Vectorization of a matrix|link]]).

#Algebra #Mathematics 