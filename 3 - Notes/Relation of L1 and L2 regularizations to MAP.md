Tags: [[__Machine_Learning]]

# Introduction
Let's remind, that MAP Estimation ([[MAP Estimation (Maximum A Posteriori)|link]]) is equivalent to minimizing a loss function with regularization as described here - [[Relation between MAP and minimizing loss with regularization]].

So MAP finds parameters $\theta$ which minimizes the negative log posterior:
$$
\theta_{MAP} = \text{arg} \min_\theta [-\log(p(D \mid \theta) - \log(p(\theta))]
$$
where:
- $-\log(p(D \mid \theta)$ - Loss function, e.g. MSE ([[MSE (Mean Squared Error)|link]]), Cross-Entropy ([[Cross-Entropy for classification|link]])
- $- \log(p(\theta))$ - Regularization penalty ([[Regularization|link]])
# Relation between MAP and L2
If we use assume, that prior is the Gaussian distribution ([[Normal (Gaussian) distribution|link]]):
$$
\begin{gather}
\theta = (\theta_1, \ldots, \theta_n) \\
\theta_i \sim \mathcal{N}(0, \sigma^2) \\
p(\theta) = \prod_{i=1}^n \frac{1}{\sqrt{2 \pi \sigma^2}}
\exp(-\frac{\theta_i^2}{2 \sigma^2}) \\
p(\theta_i) = \frac{1}{\sqrt{2 \pi \sigma^2}}
\exp(-\frac{\theta_i^2}{2 \sigma^2}) \\
\end{gather}
$$
that means, that the prior is proportional ([[Proportionality|link]]) to:
$$
\Large
p(\theta_i) \propto e^{-\theta_i^2}
$$
then regularization penalty $- \log(p(\theta))$ from the negative log posterior is proportional to the penalty from L2 regularization:
$$
-\log(p(\theta)) \propto \lVert \theta \rVert_2^2
$$
## Proof
The above proportionality:
$$
-\log(p(\theta)) \propto \lVert \theta \rVert_2^2
$$
is caused by the fact that:
$$
\begin{align}
 & p(\theta) = \prod_{i=1}^n \frac{1}{\sqrt{2 \pi \sigma^2}}
\exp(-\frac{\theta_i^2}{2 \sigma^2}) \\
 & -\log(p(\theta)) = -\sum_{i=1}^n \log(\frac{1}{\sqrt{2 \pi \sigma^2}})
- \sum_{i=1}^n \frac{\theta_i^2}{2 \sigma^2}
\end{align}
$$
If we get rid of the constants $\large \log(\frac{1}{\sqrt{2 \pi \sigma^2}})$ and $\large \frac{1}{2 \sigma^2}$, we are left with:
$$
-\log(p(\theta)) \propto \sum_{i=1}^n \theta_i^2 = \lVert \theta_i \rVert^2_2
$$
# Relation between MAP and L1
If we assume, that prior is the Laplace distribution ([[Laplace distribution|link]]):
$$
\begin{gather}
\theta = (\theta_1, \ldots, \theta_n) \\
\theta_i \sim \mathcal{L}(0, b) \\
p(\theta) = \prod_{i=1}^n \frac{1}{2b}
\exp(-\frac{|\theta_i|}{b}) \\
p(\theta_i) = \frac{1}{2b}
\exp(-\frac{|\theta_i|}{b}) \\
\end{gather}
$$
that means, that the prior is proportional ([[Proportionality|link]]) to:
$$
\Large
p(\theta_i) \propto e^{-|\theta_i|}
$$
then regularization penalty $- \log(p(\theta))$ from the negative log posterior is proportional to the penalty from L1 regularization:
$$
-\log(p(\theta)) \propto \lVert \theta \rVert_1
$$
## Proof
The above proportionality:
$$
-\log(p(\theta)) \propto \lVert \theta \rVert_1
$$
Can be proved analogically as in the section 'Relation between MAP and L2' above.

#MachineLearning 