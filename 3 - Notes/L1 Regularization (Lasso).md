Tags: [[__Machine_Learning]]

# Introduction
L1 (Lasso) Regularization is a type of regularization ([[Regularization|link]]) where we add a penalty proportional to the sum of **absolute values** of model parameters:
$$
Loss_{reg}(\theta) = Loss(\theta) + \lambda \lVert \theta \rVert_1
$$
where:
- $\theta = (\theta_1, \ldots, \theta_n)$ - Model's parameters
- $\lVert \theta \rVert_1 = \sum_{i=1}^n |\theta_i|$ 
- $\lambda \ge 0$ - Regularization strength (chosen parameter)

It makes the model to have smaller parameters what prevents relying too much on a single feature based on which we make predictions ([[Dataset of observations of random variables X, Y - Variables per sample, feature and target variable|link]]).

Unlike L2 regularization ([[L2 Regularization (Ridge)|link]]), it has a tendency to produce sparse models, that is models with a small number of parameters, by reducing some of the parameters to zero.

Features for which corresponding parameters are reduced to zero, doesn't make any impact on predictions, so L1 helps with selecting those features which matters while ignoring others.

When we have two correlated features, L1 usually reduces parameters corresponding to one of them to zero.

Sparse models are simpler, easier to interpret, and often generalize better.
# Derivation
When training models, we minimize the loss using derivatives (e.g., gradient descent) ([[Gradient Descent - ML|link]]). 

We update parameters in iterations, by subtracting from them a value relative to the derivative of a loss function in each iteration.

For L1, the penalty formula is not continuous so it doesn't have a standard derivative. Instead, we use the subgradient:
$$
\frac{\partial}{\partial \theta_j} \lambda |\theta_j| = \lambda \cdot sign(\theta_j) = \begin{cases}
+ \lambda, \quad \theta_j > 0 \\
- \lambda, \quad \theta_j < 0 \\
\text{undefined (subgradient)}, \quad \theta_j = 0 \\
\end{cases}
$$
So gradient of the regularized loss becomes:
$$
\frac{\partial Loss_{reg}}{\partial \theta_j} = \frac{\partial Loss}{\partial \theta_j} + \frac{\partial}{\partial \theta_j} \lambda |\theta_j| =
\frac{\partial Loss}{\partial \theta_j} + \lambda \cdot sign(\theta_j)
$$
In gradient descent, this gives the rule for updating parameters:
$$
\theta_j^{new} = \theta_j - \eta (\frac{\partial Loss}{\partial \theta_j} + \lambda \cdot sign(\theta_j))
$$
This means:
- In each iteration, we update parameters by at least $\lambda$ 
- We don't make smaller and smaller updates like in case of L2 regularization
- When parameter is small, it can be easily reduced to 0
- That's why L1 has a tendency to produce sparse models, unlike L2 regularization
# Geometric interpretation
L1 regularization adds a penalty:
$$
\lambda \lVert \theta \rVert_1 = \lambda(|\theta_1| + \ldots + |\theta_n|)
$$
Finding a minimum of a loss with a penalty:
$$
\min_\theta Loss(\theta) + \lambda \lVert \theta \rVert_1
$$
is equivalent to finding a minimum of a loss with a constraint:
$$
\min_\theta Loss(\theta) \text{, where } \lVert \theta \rVert_1 \le c
$$
for some value $c$.

Set of parameters that satisfies the constraint $\lVert \theta \rVert_1 \le c$ is a **diamond-shaped polytope** in 2D and a **cross-polytope** in n dimensions.  

It has **sharp corners**, and these corners lie on axes — this is why the optimum often occurs at points where many parameters are **exactly zero**.

The exact value of $c$ is only hypothetical, we don't know its value until the minimum is found, and it depends on $\lambda$:
- Larger $\lambda$ → smaller feasible region → more parameters forced to zero
- Smaller $\lambda$ → larger feasible region → fewer parameters set to zero

Once minimum of the loss with a penalty is found, then we can calculate $c$ and it is such a value, that set of parameters satisfying $\lVert \theta \rVert_1 = c$ is a polytope which touches the loss function curve.
# Properties
Below are described properties of L1 regularization.
## Produces sparse models (feature selection)
L1 has a tendency to produce sparse models, that is models with a small number of parameters, by setting value of some parameters to zero.

That's because the derivative of the penalty $\lambda |\theta_i|$ is $\lambda$, which is constant. So we are updating parameters by at least $\eta \lambda$. 

When value of a parameter is getting close to zero, updates which we make are not getting close to zero, so parameter can be easily reduced to zero.

This is described in more detail in the 'Derivation' section earlier in this document.
## Creates simpler and more interpretable models
Because many parameters become exactly zero, the model effectively performs **feature selection**. Features for which parameters has been reduced to zero, doesn't make any impact on predictions.

This is highly desirable in high-dimensional datasets and leads to a better generalization (prevents overfitting).
## Non-continuous loss (non-differentiable at 0)
The derivative of $|\theta_i|$ is $\text{sign}(\theta_i)$ which jumps abruptly at 0 and it is non-continuous (thus non-differentiable) at that point.

Optimization requires subgradients or specialized algorithms (e.g., coordinate descent).
## Does **not** necessarily produce similar weights for correlated features
When we have two correlated features, then unlike L2, L1 tends to push parameters corresponding to one of those features more aggressively towards zero, so parameters for the other feature might stay relatively big.
## Big gradients
For two correlated features, L1 might leave parameters corresponding to one of the features much bigger then for the other feature, like described in the previous section.

That can cause gradients to be big and with big gradients, updating parameters is unstable because we update values of parameters by a lot. 

If we update parameters by a lot, then we might miss the optimal value. For example we update a parameter from 2 to 6 while the optimum was 3.
## Solutions are not always unique
- Because of non-smoothness and sparsity, multiple equally good sparse solutions may exist.
- Common when features are highly correlated.
# Relation to MAP estimation

#MachineLearning 