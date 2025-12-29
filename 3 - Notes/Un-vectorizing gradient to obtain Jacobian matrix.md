Tags: [[__Mathematics]], [[_Mathematical_analysis]]
#MathematicalAnalysis #Mathematics 
# Introduction
If $f$ is a function which takes a matrix as an input as returns a scalar as an output:
$$
f: \mathbb{R}^{m \times n} \rightarrow \mathbb{R}
$$
then:
$$
\large
\text{unvec} \left( \nabla_{\text{vec}(x)} f \right) = 
\frac{\partial f}{\partial x} = J_x f, 
\quad x \in \mathbb{R}^{m \times n},
\quad \text{vec}(x) \in \mathbb{R}^{m n}
$$
where:
- $\large \nabla_{\text{vec}(x)} f$ - Gradient
- $\large \frac{\partial f}{\partial x} = J_x f$ - Jacobian matrix
- vec() is vectorization of a matrix ([[Vectorization of a matrix|link]]) 
- unvec() is converting a vector back into a matrix
# Visualization
$$
\large
x = \begin{pmatrix}
x_{11} & \ldots & x_{1n} \\
\vdots & \ddots & \vdots \\
x_{m1} & \ldots & x_{mn} \\
\end{pmatrix}
\quad
\text{vec}(x) = \begin{pmatrix}
x_{11} \\
\vdots \\
x_{m1} \\
\vdots \\
x_{1n} \\
\vdots \\
x_{mn}
\end{pmatrix}
$$
$$
\large
\frac{\partial f}{\partial x} = J_x(f) = \begin{pmatrix}
\frac{\partial f}{\partial x_{11}} & \dots & \frac{\partial f}{\partial x_{1n}} \\
\vdots & \ddots & \vdots \\
\frac{\partial f}{\partial x_{m1}} & \dots & \frac{\partial f}{\partial x_{mn}} \\
\end{pmatrix},
 
\quad
 
\large
\nabla_{\text{vec}(x)} f = \begin{pmatrix}
\frac{\partial f}{\partial x_{11}} \\
\vdots \\
\frac{\partial f}{\partial x_{m1}} \\
\vdots \\
\frac{\partial f}{\partial x_{1n}} \\
\vdots \\
\frac{\partial f}{\partial x_{mn}}
\end{pmatrix}
$$
