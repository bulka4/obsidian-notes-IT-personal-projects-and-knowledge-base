Tags: [[__Mathematics]], [[_Mathematical_analysis]]
#MathematicalAnalysis #Mathematics 

# Introduction
If we have a function $f$ with a vector as an input and scalar as an output:
$$
\large f: \mathbb{R}^{k} \rightarrow \mathbb{R}
$$
then its Jacobian matrix for the input $x \in \mathbb{R}^k$ is:
$$
\Large
\frac{\partial f}{\partial x}(x) = J_x(f) = \begin{pmatrix}
\frac{\partial f}{\partial x_{1}}(x) & \dots & \frac{\partial f}{\partial x_{k}}(x)
\end{pmatrix}
$$
# Notation using gradient
When Jacobian is a single row, it can be also written as a transposed gradient vector ([[Gradient vector|link]]):
$$
\Large
J_x(f) = \begin{pmatrix}
\frac{\partial f}{\partial x_1}(x) & \dots & \frac{\partial f}{\partial x_n}(x)
\end{pmatrix}
= (\nabla_x f)^T
$$
