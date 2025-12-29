Tags: [[__Machine_Learning]]

# Introduction
Padding is an operation where we add zero rows and columns to a 2-D or a 3-D tensor which is an input for a machine learning model.

Padding is defined as a pair $(p_h, p_w)$ such that:
- $p_h$ - How many rows add to the top and bottom (that increases the height of the input)
- $p_w$ - How many columns add to the left and right (that increases the width of the input)

For example, for a given input tensor $X \in \mathbb{R}^{3 \times 3 \times C}$, its padded version $X_{\text{pad}} \in \mathbb{R}^{5 \times 5 \times C}$ for $p_h = p_w = 1$ looks like this:
$$
X = \begin{pmatrix}
x_{11} & x_{12} & x_{13} \\
x_{21} & x_{22} & x_{23} \\
x_{31} & x_{32} & x_{33} \\
\end{pmatrix}
, \quad
X_{\text{pad}} = \begin{pmatrix}
0 & 0 & 0 & 0 & 0 \\
0 & x_{11} & x_{12} & x_{13} & 0 \\
0 & x_{21} & x_{22} & x_{23} & 0 \\
0 & x_{31} & x_{32} & x_{33} & 0 \\
0 & 0 & 0 & 0 & 0 \\
\end{pmatrix}
$$
To be precise, padding changes patch $X$ into $X_{\text{pad}}$ , such that:
$$
\large \begin{align}
& X_{\text{pad}} \in \mathbb{R}^{(H_{\text{in}} + 2p_h) \times (W_{\text{in}} + 2 p_w) \times C_{\text{in}}} \\
& X_{\text{pad}} = \begin{cases}
X[i - p_h,\ j - p_w,\ c] & 
\text{if } 1 \le i - p_h \le H_{\text{in}} \wedge 1 \le j - p_w \le W_{\text{in}} \\
0 & \text{otherwise}
\end{cases}
\end{align}
$$

This technique if often used together with data patching ([[Data patching|link]]) for example in a convolution neural network layer.

#MachineLearning 