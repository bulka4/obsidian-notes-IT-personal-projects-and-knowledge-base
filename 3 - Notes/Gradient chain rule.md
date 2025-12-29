Tags: [[__Mathematics]], [[_Mathematical_analysis]]

# Introduction
Gradient chain rule is a special case of the Jacobian chain rule (described here - [[Jacobian chain rule|link]]), when the final function is a scalar one.
# Gradient chain rule
Let's assume, that:
- $x \in \mathbb{R}^{n_0}$ 
- $f^{(1)}, \ldots, f^{(k)}$ - Differentiable functions
- Each $\large f^{(i)}: \mathbb{R}^{n_{i - 1}} \rightarrow \mathbb{R}^{n_i}$ 
- We have intermediate variables defined as:
$$
x^{(0)} = x, \qquad x^{(i)} = f^{(i)}(x^{(i-1)}), \qquad i = 1, \ldots, k
$$
- Scalar variable $L \in \mathbb{R}$ is the final one, which is an output of the function $l$:
$$
L = l(x^{(k)}) \in \mathbb{R}
$$

and gradient ([[Gradient vector|link]]) of the final variable $L$ is:
$$
\Large
\nabla_x L = J_{x^{(0)}}(x^{(1)})^T \dots J_{x^{(k-1)}}(x^{(k)})^T \nabla_{x^{(k)}}L
$$
where Jacobian matrix of $x^{(i)}$ is:
$$
\Large
J_{x^{(i-1)}}(x^{(i)}) = \frac{\partial x^{(i)}} {\partial x^{(i-1)}} =
\frac{\partial f^{(i)}} {\partial x^{(i-1)}} =
\begin{pmatrix}
\frac{\partial x^{(i)}_1}{\partial x^{(i-1)}_1} & \ldots & \frac{\partial x^{(i)}_1}{\partial x^{(i-1)}_{n_{i-1}}} \\
\vdots & \ddots & \vdots \\
\frac{\partial x^{(i)}_{n_{i}}}{\partial x^{(i-1)}_1} & \ldots & \frac{\partial x^{(i)}_{n_{i}}}{\partial x^{(i-1)}_{n_{i-1}}} \\
\end{pmatrix}
$$
and gradient is:
$$
\Large
\nabla_x L = \begin{pmatrix}
\frac{\partial L}{\partial x_1} \\
\vdots \\
\frac{\partial L}{\partial x_{n_{(0)}}}
\end{pmatrix}
$$
# Derivation from the Jacobian chain rule
Jacobian for the variable $L$ is a transposed gradient vector:
$$
\Large
J_{x^{(k)}}(L) = (\nabla_{x^{(k)}}L)^T
$$
Jacobian chain rule gives us:
$$
\Large
J_{x^{(0)}}(L) = J_{x^{(k)}}(L) J_{x^{(k-1)}}(x^{(k)}) \dots J_{x^{(0)}}(x^{(1)})
$$
Using gradient notation that is:
$$
\Large
(\nabla_x L)^T = (\nabla_{x^{(k)}} L)^T J_{x^{(k-1)}}(x^{(k)}) \dots J_{x^{(0)}}(x^{(1)})
$$
If we transpose the entire equation, that gives:
$$
\Large
\nabla_x L = J^T_{x^{(0)}}(x^{(1)}) \dots J^T_{x^{(k-1)}}(x^{(k)}) \nabla_{x^{(k)}}L
$$
# Interpretation
Interpretation is the same as described in this document - [[Jacobian chain rule]].

#MathematicalAnalysis #Mathematics  