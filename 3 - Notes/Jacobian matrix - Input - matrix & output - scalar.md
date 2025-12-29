Tags: [[__Mathematics]], [[_Mathematical_analysis]]
#MathematicalAnalysis #Mathematics 

# Introduction
If we have a function $f$ with a matrix as an input and scalar as an output:
$$
\large f: \mathbb{R}^{k \times l} \rightarrow \mathbb{R}
$$
and argument $\large x \in \mathbb{R}^{k \times l}$ :
$$
x = \begin{pmatrix}
x_{11} & \ldots & x_{1l} \\
\vdots & \ddots & \vdots \\
x_{k1} & \ldots & x_{kl} \\
\end{pmatrix}
$$
Then Jacobian matrix for that function w.r.t. to the argument $x$ is:
$$
\Large
\frac{\partial f}{\partial x}(x) = J_x(f) = \begin{pmatrix}
\frac{\partial f}{\partial x_{11}}(x) & \dots & \frac{\partial f}{\partial x_{1l}}(x) \\
\vdots & \ddots & \vdots \\
\frac{\partial f}{\partial x_{k1}}(x) & \dots & \frac{\partial f}{\partial x_{kl}}(x) \\
\end{pmatrix}
$$
## Vectorized form
We can also vectorize $x$ and then we get:
$$
\Large
\begin{align}
& \frac{\partial f}{\partial \text{vec}(x)}(x) = J_{\text{vec}(x)}(f) = \\
& \quad = \begin{pmatrix}
\frac{\partial f}{\partial x_{11}}(x) & \dots & \frac{\partial f}{\partial x_{k1}}(x)
& \dots & \frac{\partial f}{\partial x_{1l}}(x) & \dots 
& \frac{\partial f}{\partial x_{kl}}(x)
\end{pmatrix}
\end{align}
$$
and un-vectorize to go back to the previous form:
$$
\large
\text{unvec}(J_{\text{vec}(x)}(f)) = J_x(f)
$$
