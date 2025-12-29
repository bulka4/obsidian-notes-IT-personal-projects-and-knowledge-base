Tags: [[__Mathematics]], [[_Mathematical_analysis]]

# Introduction
Let's assume, that:
- $x \in \mathbb{R}^{n_0}$ - Constant value
- $F = f^{(k)} \circ f^{(k-1)} \circ \ldots \circ f^{(1)}$ - Composition of functions
- $\Large f^{(i)}: \mathbb{R}^{n_{i - 1}} \rightarrow \mathbb{R}^{n_i}$ 
- Intermediate variables are:
$$
\begin{align}
& x^{(0)} = x, & x^{(1)} = f^{(1)}(x^{(0)}), & \ldots, & x^{(k)} = f^{(k)}(x^{(k-1)})
\end{align}
$$
	with shapes:
$$
\large
x^{(i)} \in \mathbb{R}^{n_i}
$$
- Jacobian matrix ([[Jacobian matrix|link]]) of $f^{(i)}$ at $x^{(i-1)}$ is:
$$
\Large
J_{x^{(i-1)}} (x^{(i)}) = \frac{\partial x^{(i)}} {\partial x^{(i-1)}} = \frac{\partial f^{(i)}} {\partial x^{(i-1)}}
$$
Then derivative of $F$ can be written as:
$$
\Large
\frac{\partial F}{\partial x} = J_{x^{(k-1)}} (x^{(k)})
J_{x^{(k-2)}} (x^{(k-1)})
\cdots
J_{x^{(0)}} (x^{(1)})
= \prod_{i=k}^1 J_{x^{(i-1)}} (x^{(i)})
$$
# How elements of the product of Jacobian matrices look like
Jacobian matrix $\Large J_{x^{(i-1)}} (x^{(i)}) = \frac{\partial x^{(i)}} {\partial x^{(i-1)}}$ looks like this:
$$
\Large \begin{pmatrix}
\frac{\partial x^{(i)}_1} {\partial x^{(i-1)}_1} & \ldots
& \frac{\partial x^{(i)}_1} {\partial x^{(i-1)}_{n_{i-1}}} \\
 
\vdots & \ddots & \vdots \\
 
\frac{\partial x^{(i)}_n} {\partial x^{(i-1)}_1} & \ldots
& \frac{\partial x^{(i)}_n} {\partial x^{(i-1)}_{n_{i-1}}} \\
\end{pmatrix}
$$
And using notes about multiplying matrices - [[Multiplication of matrices|link]] - we have a recursive formula for the element in the $m$-th row and $l$-th column:
$$
\Large
(\frac{\partial F}{\partial x})_{ml} = (B^{(k)})_{ml} = 
\sum_{j=1}^{n^{(k-1)}} (B^{(k-1)})_{mj} \cdot 
\frac{\partial x^{(k)}_j}{\partial x^{(k-1)}_l}
$$
where:
$$
\Large
B^{(k)} = J_{x^{(k-1)}} (x^{(k)}) \ldots J_{x^{(0)}} (x^{(1)})
$$
and in non-recursive form:
$$
\Large
(B^{(k)})_{ml} = \sum_{i_1}^{n^{(k-1)}} \ldots \sum_{i_{k-1}}^{n^{(1)}}
\frac{\partial x^{(1)}_m}{\partial x^{(0)}_{i_1}}
\frac{\partial x^{(2)}_{i_1}}{\partial x^{(1)}_{i_2}}
\ldots
\frac{\partial x^{(k)}_{i_{k-1}}}{\partial x^{(k-1)}_{l}}
$$
or shortly:
$$
\huge
(B^{(k)})_{ml} = \sum_{i_1, \ldots, i_{k-1}} \prod_{t=1}^k 
\frac{\partial x^{(t)}_{i_{t-1}}}{\partial x^{(t-1)}_{i_t}}
$$
where:
- $i_0 = m$ 
- $i_k = l$ 
# Interpretation
Composed function:
$$
F = f^{(k)} \circ f^{(k-1)} \circ \ldots \circ f^{(1)}
$$
represents a chain of dependencies between functions:
- $F$ depends on $f^{(k)}$ 
- $f^{(k)}$ depends on $f^{(k-1)}$ 
- and so on

That means that:
- $F$ depends not only on $f^{(k)}$ but also on $f^{(i)}$ for every $i = 1, \ldots, k$ 
- Values $x^{(k)}$ are dependent on $x^{(k-1)}$ as well
- $x^{(1)}$ doesn't depend on any function, it depends only on $x^{(0)}$ which is a constant

A single Jacobian matrix:
$$
\Large
J_{x^{(i-1)}} (x^{(i)}) = \frac{\partial x^{(i)}} {\partial x^{(i-1)}} = \frac{\partial f^{(i)}} {\partial x^{(i-1)}}
$$
tells us what is a dependency between $f^{(i)}$ and $x^{(i-1)}$, whether increasing value of $x^{(i-1)}$ causes an increase or a decrease of the value of $f^{(i)}$.

So, in this equation:
$$
\large
\frac{\partial F}{\partial x} = J_{x^{(k-1)}} (x^{(k)})
J_{x^{(k-2)}} (x^{(k-1)})
\cdots
J_{x^{(0)}} (x^{(1)})
$$
- $\large \frac{\partial F}{\partial x}$ represents dependency between $F$ and $x = x^{(0)}$ 
- $\large J_{x^{(k-1)}} (x^{(k)})$ Represents dependency of $x^{(k)}$ on $x^{(k-1)}$ for every $k$ 

so dependency between $F$ and $x = x^{(0)}$ is represented using a chain of dependencies between $x^{(k)}$ on $x^{(k-1)}$ for every $k$.

#MathematicalAnalysis #Mathematics 