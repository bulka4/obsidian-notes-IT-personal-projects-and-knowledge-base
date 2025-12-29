Tags: [[_Algebra]], [[__Mathematics]]

# Introduction
Let's assume, that:
- $A, B, X$ - matrices
- vec() - Vectorization of a matrix ([[Vectorization of a matrix|link]])
- $\otimes$ - Kronecker product ([[Kronecker product|link]])

Then we the following equations are true:
$$
\begin{align}
& \text{vec}(AXB^T) = (B \otimes A)\text{vec}(X) \\
& \text{vec}(AB) = \text{vec}(IAB) = (B^T \otimes I)\text{vec}(A) \\
& \text{vec}(AB) = \text{vec}(ABI) = (I \otimes A)\text{vec}(B) \\
\end{align}
$$

#Algebra #Mathematics 