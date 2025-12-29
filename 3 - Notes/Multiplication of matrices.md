Tags: [[_Algebra]], [[__Mathematics]]

# Introduction
If we have two matrices of shapes $A: (m, n),\ B: (n, l)$:
$$
\begin{align}
& A = (a_{ij})_{m \times n} =  \begin{pmatrix}
a_{11} & \ldots & a_{1n} \\
\vdots & \ddots & \vdots \\
a_{m1} & \ldots & a_{mn} \\
\end{pmatrix}
 
& B = (b_{ij})_{n \times l} = \begin{pmatrix}
b_{11} & \ldots & b_{1l} \\
\vdots & \ddots & \vdots \\
b_{n1} & \ldots & b_{nl} \\
\end{pmatrix}
\end{align}
$$
Then when we multiply them, we **multiply rows** of $A$ **by columns** of $B$. 

So in order to be able to multiply matrices $A$ by $B$, **number of columns in** $A$ must be equal, to **number of rows in** $B$.

After multiplication, we receive the **product which has a shape** $(m, l)$ and looks like that:
$$
\large
A \cdot B = \begin{pmatrix}
\sum_{i=1}^n a_{1i} b_{i1} & \ldots & \sum_{i=1}^n a_{1i} b_{il} \\
\vdots                     & \ddots & \vdots \\
\sum_{i=1}^n a_{mi} b_{i1} & \ldots & \sum_{i=1}^n a_{mi} b_{il} \\
\end{pmatrix}
$$
So element from the $i$-th row and $j$-th column $(A \cdot B)_{i,j}$ consists of elements from the $i$-th row of matrix $A$ and $j$-th column of matrix $B$:
$$
\large
(A \cdot B)_{i,j} = \sum_{k=1}^n a_{ik} b_{kj}
$$
# Multiplying multiple matrices
If we want to multiply many matrices $A^{(1)}, \ldots, A^{(n)}$, where 
$$
\Large A^{(k)} = (a^{(k)}_{ij})_{n^{(k-1)} \times n^{(k)}}
$$
Shapes need to look like that because when multiplying $A^{(k)} \cdot A^{(k+1)}$ we multiply shapes this way:
$$
(n^{(k-1)}, n^{(k)}) \cdot (n^{(k)}, n^{(k + 1)}) = (n^{(k-1)}, n^{(k+1)})
$$
which is correct, that is number of columns of $A^{(k)}$ equals to number of rows of $A^{(k+1)}$.

Let's define:
$$
\begin{align}
& B^{(1)} = A^{(1)} \\
& B^{(m)} = B^{(m-1)} \cdot A^{(m)},\ m \ge 2 \\
& B^{(m)} = A^{(1)} \ldots A^{(m)}
\end{align} 
$$
Then we have a recursive formula for elements of $B^{(m)}$ :
$$
\Large
(B^{(m)})_{kl} = \sum_{j=1}^{n^{(m-1)}} (B^{(m-1)})_{kj} \cdot a_{jl}^{(m)}
$$
and $B^{(m)}$ has shape $(n^{(0)}, n^{(m)})$.

Or in non-recursive form:
$$
\Large
(B^{(m)})_{kl} = \sum_{i_1}^{n^{(m-1)}} \ldots \sum_{i_{m-1}}^{n^{(1)}}
a_{k i_1}^{(1)} a_{i_1 i_2}^{(2)} \ldots a_{i_{m-1} l}^{(m)}
$$
or shortly:
$$
\huge
(B^{(m)})_{kl} = \sum_{i_1, \ldots, i_{m-1}} \prod_{t=1}^m 
a_{i_{t-1} i_t}^{(t)}
$$
where:
- $i_0 = k$ 
- $i_k = l$ 
## Explanation
This section shows how to derive the above formula recursively and how matrices look like.

First, let's multiply the first two matrices:
$$
\large
A^{(1)} \cdot A^{(2)} = B^{(2)} = \begin{pmatrix}
\sum_{i=1}^{n^{(1)}} a^{(1)}_{1i} a^{(2)}_{i1} & \ldots & 
\sum_{i=1}^{n^{(1)}} a^{(1)}_{1i} a^{(2)}_{i n^{(2)}} \\
 
\vdots & \ddots & \vdots \\
 
\sum_{i=1}^{n^{(1)}} a^{(1)}_{n^{(0)} i} a^{(2)}_{i1} & \ldots & 
\sum_{i=1}^{n^{(1)}} a^{(1)}_{n^{(0)} i} a^{(2)}_{i n^{(2)}} \\
\end{pmatrix}
\text{ - shape } (n^{(0)}, n^{(2)})
$$
Let's denote:
$$
\large
(B^{(2)})_{kl} = \sum_{i=1}^{n^{(1)}} a^{(1)}_{ki} a^{(2)}_{il}
$$
Now let's multiply the next matrix:
$$
\large
A^{(1)} \cdot A^{(2)} \cdot A^{(3)} = B^{(2)} \cdot A^{(3)} = B^{(3)}
$$
$$
\large
B^{(3)} = \begin{pmatrix}
\sum_{j=1}^{n^{(2)}} (B^{(2)})_{1j} \cdot a^{(3)}_{j1} & \ldots 
& \sum_{j=1}^{n^{(2)}} (B^{(2)})_{1j} \cdot a^{(3)}_{j n^{(3)}} \\
 
\vdots & \ddots & \vdots \\
 
\sum_{j=1}^{n^{(2)}} (B^{(2)})_{n^{(0)} j} \cdot a^{(3)}_{j1} & \ldots 
& \sum_{j=1}^{n^{(2)}} (B^{(2)})_{n^{(0)} j} \cdot a^{(3)}_{j n^{(3)}} \\
\end{pmatrix}
 
\text{ - shape } (n^{(0)}, n^{(3)})
$$
Its elements are:
$$
\large
(B^{(3)})_{kl} = \sum_{j=1}^{n^{(2)}} (B^{(2)})_{kj} \cdot a^{(3)}_{jl} =
\sum_{j=1}^{n^{(2)}} 
\left( \sum_{i=1}^{n^{(1)}} a^{(1)}_{ki} a^{(2)}_{ij} \right)
\cdot a^{(3)}_{jl}
$$
So recursively, we have:
$$
\Large
(B^{(m)})_{kl} = \sum_{j=1}^{n^{(m-1)}} (B^{(m-1)})_{kj} \cdot a_{jl}^{(m)}
$$
Or in non-recursive form:
$$
\Large
(B^{(m)})_{kl} = \sum_{i_1}^{n^{(m-1)}} \ldots \sum_{i_{m-1}}^{n^{(1)}}
a_{k i_1}^{(1)} a_{i_1 i_2}^{(2)} \ldots a_{i_{m-1} l}^{(m)}
$$

#Algebra #Mathematics 