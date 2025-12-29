Tags: [[__Mathematics]], [[_Probability]]

# Notation and shorthands
This document uses notation and shorthands which are described here - [[Mathematical general notations and shorthands|link]].
# Introduction
Let's assume, that:
- $Y$ and $X$ are multivariate random variables ([[Multivariate random variable|link]]):
$$
\large
\begin{gathered}
Y = (Y_1, \ldots, Y_n): (\Omega, \mathcal{F}) \rightarrow (\prod_{i=1}^n \mathcal{Y}_i,\ \bigotimes_{i=1}^n \mathcal{B}_{\mathcal{Y}_i}) \\
X = (X_1, \ldots, X_m): (\Omega, \mathcal{F}) \rightarrow (\prod_{i=1}^m \mathcal{X}_i,\ \bigotimes_{i=1}^m \mathcal{B}_{\mathcal{X}_i})
\end{gathered}
$$
- Probability distributions ([[Probability distribution|link]], [[Conditional probability distribution|link]]) $\Large P_{Y_{1:n} \mid X_{1:m}}$,  $\Large P_{X_{1:m}, Y_{1:n}}$ and $\Large P_{X_{1:m}}$ are absolutely continuous with respect to the corresponding product measures ([[Product measure|link]]):
$$
\Large
\begin{align}
P_{X_{1:m}, Y_{1:n}} & \rightarrow \large \mu = \mu_X \otimes \mu_Y \\
P_{X_{1:m}} & \rightarrow \large \mu_X = \mu_{\mathcal{X}_1} \otimes \ldots \otimes \mu_{\mathcal{X}_m} \\
P_{Y_{1:n} \mid X_{1:m}} & \rightarrow \large \mu_Y = \mu_{\mathcal{Y}_1} \otimes \ldots \otimes \mu_{\mathcal{Y}_n}
\end{align}
$$
- Those measures are defined on the corresponding product measurable spaces: 
$$
\large
\begin{align}
 & \mu: (
	 (\prod_{i=1}^m\mathcal{X}_i)
	 \times (\prod_{i=1}^n \mathcal{Y}_i)
 ,\ (\bigotimes_{i=1}^m \mathcal{B}_{\mathcal{X}_i})
	\times
	(\bigotimes_{i=1}^n \mathcal{B}_{\mathcal{Y}_i})
) \\
 & \mu_X: (\prod_{i=1}^m\mathcal{X}_i,\ \bigotimes_{i=1}^m \mathcal{B}_{\mathcal{X}_i}) \\
 & \mu_Y: (\prod_{i=1}^n \mathcal{Y}_i,\ \bigotimes_{i=1}^n \mathcal{B}_{\mathcal{Y}_i}) \\
 & \mu_{\mathcal{X}_i}: (\mathcal{X}_i, \mathcal{B}_{\mathcal{X}_i}) \\
 & \mu_{\mathcal{Y}_i}: (\mathcal{Y}_i, \mathcal{B}_{\mathcal{Y}_i})
\end{align}
$$

Then, from the definition of the conditional probability distribution we can derive the formula for conditional probability distribution function:
$$
\Large
p_{Y_{1:n} \mid X_{1:m}}(y_{1:n} \mid x_{1:m}) = \frac{ p_{X_{1:m}, Y_{1:n}}(x_{1:m}, y_{1:n}) }{p_{X_{1:m}}(x_{1:m})}
$$
for all $\large x_{1:m}$, such that $\Large p_{X_{1:m}}(x_{1:m}) > 0$.

#Mathematics #Probability 