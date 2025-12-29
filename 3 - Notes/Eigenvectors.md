Tags: [[_Algebra]], [[__Mathematics]]

# Introduction
Most of the vectors ([[Vector|link]]), after applying on them a linear transformation (multiplying them by a matrix), will change their direction ([[Direction of a vector|link]]).

Eigenvectors on the other hand, they only get stretched or compressed, so their length changes.

They are always define with respect to a specific matrix.
# Definition
Eigenvector with respect to the matrix $A$, is such a vector $v$, that there exists $\lambda$ such that:
$$
Av = \lambda v
$$
where $\lambda$ is called the eigenvalue of that vector.

- If $\lambda > 1$, then vector $v$ is stretched
- If $0 < \lambda < 1$, then vector $v$ is shrunk
- If $\lambda < 0$, then vector $v$ has flipped direction
# How to find eigenvectors for a matrix
For a given matrix $A$, we can find its corresponding eigenvectors by solving the equation:
$$
\begin{align}
& Av = \lambda v \\
& (A - \lambda I)v = 0
\end{align}
$$
For a non-zero solution $v$, the determinant must be zero:
$$
\text{det}(A - \lambda I) = 0
$$

That gives us eigenvalues $\lambda$.

Then, we use each eigenvalue in this equation:
$$
(A - \lambda I)v = 0
$$
and solve it to find corresponding eigenvector $v$.
# Interpretation
Vector can be interpreted as a direction as described here - [[Direction of a vector]].

Matrix represents a linear transformation ([[Matrix as a linear transformation|link]]). When applied to a vector (multiplied by a vector), it can stretch, shrink or rotate that vector.

Eigenvectors and eigenvalues describe which vectors have their directions either stretched or shrunk, without rotating (changing direction) and by how much.

#Algebra #Mathematics 