Tags: [[__Mathematics]], [[_Mathematical_analysis]]

# Introduction
If:
- $W$ - size $(m, n)$ 
- $a$ - size $(n, 1)$ 

Then the following formula is true:
$$
\frac{\partial (Wa)} {\partial \text{vec}(W)} = a^T \otimes I
$$
## Proof
### Version 1
The above formula is true because, as mentioned here - [[Matrix vectorization identity|link]], we have a property:
$$
\text{vec}(AB) = \text{vec}(IAB) = (B^T \otimes I)\text{vec}(A)
$$
so:
$$
\text{vec}(Wa) = (a^T \otimes I_m)\text{vec}(W)
$$
Since $Wa$ has shape $(m, n) \cdot (n, 1) = (m, 1)$, then $\text{vec}(Wa) = Wa$, so:
$$
Wa = (a^T \otimes I_m)\text{vec}(W)
$$
and if we differentiate both sides, that gives:
$$
\frac{\partial (Wa)} {\partial \text{vec}(W)} = a^T \otimes I_m
$$
### Version 2
We can also proof the same another way. Let's denote: $z = Wa$. A derivative for a single element is:
$$
\large 
z_i = \sum_{j=1}^{n} W_{ij} a_j
$$
$$
\large
\frac{\partial z_i}{\partial W_{pq}} = 
\begin{cases}
a_q  & i=p \\
0 & i \neq p
\end{cases}
$$
Since $\large J_{W} (z)$ looks like that:
$$
\Large
J_{W} (z) = \begin{bmatrix}
\frac {\partial z_1} {\partial W_{11}} & \ldots & 
\frac {\partial z_1} {\partial W_{m 1}} & \ldots &
\frac {\partial z_1} {\partial W_{1 n}} & \ldots & 
\frac {\partial z_1} {\partial W_{mn}} \\
\vdots & \ddots & \vdots & \ddots & \vdots & \ddots & \vdots \\
\frac {\partial z_m} {\partial W_{11}} & \ldots & 
\frac {\partial z_m} {\partial W_{m 1}} & \ldots &
\frac {\partial z_m} {\partial W_{1 n}} & \ldots & 
\frac {\partial z_m} {\partial W_{mn}} \\
\end{bmatrix}
$$
and $\large a^T \otimes I_m$ looks like that:
$$
\large
\begin{bmatrix}
a_1 & 0 & \ldots & 0 & \ldots &
a_n & 0 & \ldots & 0 \\
0 & \ddots & 0 & \vdots & \ldots & 0 & \ddots & 0 & \vdots \\
\vdots & 0 & \ddots & 0 & \ldots & \vdots & 0 & \ddots & 0 \\
0 & \ldots & 0 & a_1 & \ldots &
0 & \ldots & 0 & a_n \\
\end{bmatrix}
$$
That means, that they are equal:
$$
\large
J_{W} (z) = J_{\text{vec}(W)} (z) = 
a^T \otimes I_m
$$

#MathematicalAnalysis #Mathematics 