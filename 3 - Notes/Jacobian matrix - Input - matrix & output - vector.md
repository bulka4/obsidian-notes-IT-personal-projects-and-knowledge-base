Tags: [[__Mathematics]], [[_Mathematical_analysis]]
#MathematicalAnalysis #Mathematics 

# Introduction
If we have a function $f$ with a matrix as an input and vector as an output:
$$
\large f: \mathbb{R}^{k \times l} \rightarrow \mathbb{R}^m
$$
and argument $\large x \in \mathbb{R}^{k \times l}$ :
$$
x = \begin{pmatrix}
x_{11} & \ldots & x_{1l} \\
\vdots & \ddots & \vdots \\
x_{k1} & \ldots & x_{kl} \\
\end{pmatrix}
$$
In order to express derivatives as a matrix, we can use vectorization ([[Vectorization of a matrix|link]]) to convert the matrix argument $x$ into a vector by stacking its columns:
$$
\text{vec}(x) = \begin{pmatrix}
x_{11} \\
\vdots \\
x_{k1} \\
x_{12} \\
\vdots \\
x_{k2} \\
\vdots \\
x_{1l} \\
\vdots \\
x_{kl} \\
\end{pmatrix}
$$
and represent derivative as a Jacobian matrix, which we denote as:
$$
\large
\frac{\partial f}{\partial x}(x) = \frac{\partial f}{\partial \text{vec}(x)}(x) = J_x(f) = J_{\text{vec}(x)}(f)
\leftarrow \text{shape } (m, kl)
$$
and it looks like that:
$$
\Large
\begin{pmatrix}
\frac{\partial f_1}{\partial x_{11}}(x) & \ldots & \frac{\partial f_1}{\partial x_{k1}}(x) & \dots
& \frac{\partial f_1}{\partial x_{1l}}(x) & \ldots 
& \frac{\partial f_1}{\partial x_{kl}}(x) \\
 
\vdots & \ddots & \vdots & \dots & \vdots & \ddots & \vdots  \\
 
\frac{\partial f_m}{\partial x_{11}}(x) & \ldots & \frac{\partial f_m}{\partial x_{k1}}(x) & \dots
& \frac{\partial f_m}{\partial x_{1l}}(x) & \ldots 
& \frac{\partial f_m}{\partial x_{kl}}(x) \\
\end{pmatrix}
$$

So element from the $i$-th row and $j$-th column is:
$$
\large
(J_x(f))_{ij} = (J_{\text{vec}(x)}(f))_{ij} = \frac{\partial f_i}{\partial \text{vec}(x)_j}(x) = \frac{\partial f_i}{\partial x_{pq}}(x)
$$
where:
- $\Large q = \left\lfloor \frac{j - 1}{k} \right\rfloor + 1$ - A floor ([[Floor of a number|link]])
- $p = j - (q - 1)k$ 

And to find a specific derivative in the Jacobian matrix:
$$
\Large
\frac{\partial f_i}{\partial x_{pq}}(x) = (J_x(f))_{i, (q-1)k + p}
$$

#MathematicalAnalysis 