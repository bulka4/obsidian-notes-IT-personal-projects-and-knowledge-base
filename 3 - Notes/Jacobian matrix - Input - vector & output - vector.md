Tags: [[__Mathematics]], [[_Mathematical_analysis]]
#MathematicalAnalysis #Mathematics 

# Introduction
For a vector valued function:
$$
\begin{align}
& f: \mathbb{R}^n \rightarrow \mathbb{R}^m,
& f(x) = 
\begin{pmatrix}
f_1(x) \\
\vdots \\
f_m(x) \\
\end{pmatrix}
\end{align}
$$
Jacobian matrix is a matrix of first-order derivatives for a specific point $x \in \mathbb{R}^n$:
$$
\Large
J_x(f) = \frac{\partial f}{\partial x}(x) = 
\begin{pmatrix}
\frac{\partial f_1}{\partial x_1}(x) & \ldots & \frac{\partial f_1}{\partial x_n}(x) \\
\vdots & \ddots & \vdots \\
\frac{\partial f_m}{\partial x_1}(x) & \ldots & \frac{\partial f_m}{\partial x_n}(x) \\
\end{pmatrix}
$$
So each row corresponds to an element from the output of $f$, and each column corresponds to an element from the input $x$ :
$$
\large
(J_x(f))_{ij} = \left( \frac{\partial f}{\partial x}(x) \right)_{ij} = 
\frac{\partial f_i}{\partial x_j}(x)
$$
