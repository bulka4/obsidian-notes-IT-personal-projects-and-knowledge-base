Tags: [[__Mathematics]], [[_Mathematical_analysis]]
#MathematicalAnalysis #Mathematics 
# Introduction
For a scalar function $f: \mathbb{R}^n \rightarrow \mathbb{R}$, gradient vector is a column vector with its derivatives for a specific point $x \in \mathbb{R}^n$:
$$
\Large
\nabla_x f = \begin{pmatrix}
\frac{\partial f}{\partial x_1}(x) \\
\vdots \\
\frac{\partial f}{\partial x_n}(x)
\end{pmatrix}
$$
# Notation using Jacobian
We can write a gradient as a transposed Jacobian matrix ([[Jacobian matrix|link]]):
$$
\Large
\nabla_x f = J^T_x(f) = \begin{pmatrix}
\frac{\partial f}{\partial x_1}(x) \\
\vdots \\
\frac{\partial f}{\partial x_n}(x)
\end{pmatrix}
$$
Other notations which we can use:
$$
\begin{align}
\large
\nabla_x f = J^T_x(f) = \left( \frac{\partial f} {\partial x}(x) \right)^T = \frac{\partial f} {\partial x^T}(x)
\end{align}
$$
