Tags: [[__Machine_Learning]]

# Introduction
Elastic Net Regularization is a type of regularization ([[Regularization|link]]) that combines both **L1 (Lasso)** ([[L1 Regularization (Lasso)|link]]) and **L2 (Ridge)** ([[L2 Regularization (Ridge)|link]]) penalties (components):
$$
Loss_{reg}(\theta) = Loss(\theta) + \lambda \lVert \theta \rVert_1 + \lambda \lVert \theta \rVert_2^2
$$
Another common form introduces a mixing parameter $\alpha \in [0,1]$:
$$
Loss_{reg}(\theta) = Loss(\theta) + \lambda (\alpha \lVert \theta \rVert_1 + (1 - \alpha) \lVert \theta \rVert_2^2)
$$
where:
- $\theta = (\theta_1, \ldots, \theta_n)$ - Model parameters
- $\lVert \theta \rVert_1 = \sum_{i=1}^n |\theta_i|$ 
- $\lVert \theta \rVert_2^2 = \sum_{i=1}^n \theta_i^2$ 
- $\lambda \ge 0$ - Regularization strength
- $\alpha$ - Controls how much of L1 vs L2 we apply

Elastic Net **combines the strengths of both L1 and L2**:
- Like **L1**, it can produce _sparse models_ (many zero parameters)
- Like **L2**, it makes gradients small (so training a model is more stable because we update parameters by a little)

It is especially useful in high-dimensional problems where:
- There are many correlated features
- L1 alone becomes unstable (big gradients)
- L2 alone does not produce sparsity
# Derivation
When training models, we minimize the loss using derivatives (e.g., gradient descent) ([[Gradient Descent - ML|link]]). 

We update parameters in iterations, by subtracting from them a value relative to the derivative of a loss function in each iteration.

Derivative of a loss with Elastic Net Regularization is:
$$
\frac{\partial Loss_{reg}}{\partial \theta_j} = 
\frac{\partial Loss}{\partial \theta_j} + 
\lambda(\alpha \frac{\partial}{\partial \theta_j} |\theta_j|
+ (1- \alpha) \frac{\partial}{\partial \theta_j}\theta_j^2)
$$
The L2 part differentiates normally:
$$
\frac{\partial}{\partial \theta_j}\theta_j^2 = 2\theta_j
$$
The L1 part does **not** have a standard derivative at 0 because it is not continuous. Instead, it uses the subgradient:
$$
\frac{\partial}{\partial \theta_j} |\theta_j| = sign(\theta_j) = \begin{cases}
+ 1, \quad \theta_j > 0 \\
- 1, \quad \theta_j < 0 \\
[-1, 1], \quad \theta_j = 0 \\
\end{cases}
$$
So the full update rule becomes:
$$
\theta_j^{new} = \theta_j - \eta (\frac{\partial Loss}{\partial \theta_j} 
+ \lambda \alpha \ \text{sign}(\theta_j)
+ 2\lambda(1- \alpha)\theta_j)
$$
Interpretation:
- L1 part: pushes parameters **abruptly toward zero**
- L2 part: shrinks all parameters **smoothly**

Elastic Net is sometimes described as:  
**“L2-stabilized L1 shrinkage.”**
# Geometric interpretation
Elastic Net regularization adds a penalty:
$$
\lambda (\alpha \lVert \theta \rVert_1 + (1 - \alpha) \lVert \theta \rVert_2^2)
$$
Finding a minimum of a loss with a penalty:
$$
\min_\theta Loss(\theta) + \lambda (\alpha \lVert \theta \rVert_1 + (1 - \alpha) \lVert \theta \rVert_2^2)
$$
is equivalent to finding a minimum of a loss with a constraint:
$$
\min_\theta Loss(\theta) \text{, where } \alpha \lVert \theta \rVert_1 + (1 - \alpha) \lVert \theta \rVert_2^2 \le c
$$
for some value $c$.

Set of parameters that satisfies the constraint $\alpha \lVert \theta \rVert_1 + (1 - \alpha) \lVert \theta \rVert_2^2 \le c$  is:
- **diamond-like (L1)** near the axes (encourages sparsity)
- **circular/elliptical (L2)** away from the axes (stabilizes correlated features)

The $c$ value is only hypothetical, we don't know it's value.

Once we find the minimum of the loss with a penalty: 
$$
\min_\theta Loss(\theta) + \lambda (\alpha \lVert \theta \rVert_1 + (1 - \alpha) \lVert \theta \rVert_2^2)
$$
that gives us parameters $\theta$ which forms the shape $\alpha \lVert \theta \rVert_1 + (1 - \alpha) \lVert \theta \rVert_2^2 \le c$ for some value $c$ which touches the loss function curve.

So before finding a minimum of the loss function with a penalty, value $c$ is only hypothetical, we don't know its value. We can only calculate it after finding the minimum of the loss function with a penalty.

Value $c$ depends on the value of $\lambda$. For smaller values of $\lambda$, we receive a bigger value $c$ because the penalty $\lambda (\alpha \lVert \theta \rVert_1 + (1 - \alpha) \lVert \theta \rVert_2^2)$ is small so it doesn't affect too much where is the minimum of the Loss.
# Properties
Below are describes properties of the Elastic Net regularization.
## Balance between L1 and L2
Elastic Net tries to balance pros and cons of both L1 and L2. The parameter $\alpha$ controls how much behavior of L1 and L2 we get.

For bigger value of $\alpha$, it behaves more like L1, while for smaller values of $\alpha$, it behaves more like L2.
## Producing sparse models
Elastic Net can set some parameters exactly to zero due to the L1 component but it does it less aggressively than L1.

The L2 component slightly reduces the tendency to set parameters to zero.
## Correlated features
When we have two correlated features, the L1 component pushes parameters for one of them towards zero and increases parameters value for the other one, while the L2 component tries to balance them.
## Gradients size
For two correlated features, the L2 component tries to keep parameters for both features low, while the L1 component reduces size of parameters related to one of the features more aggressively, so parameters for the other feature can stay bigger than in case of L2.

Bigger parameters causes bigger gradients and with big gradients, updating parameters is unstable because we update values of parameters by a lot. 

If we update parameters by a lot, then we might miss the optimal value. For example we update a parameter from 2 to 6 while the optimum was 3.
# Relation to MAP estimation

#MachineLearning 