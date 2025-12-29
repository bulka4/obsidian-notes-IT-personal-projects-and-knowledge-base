Tags: [[__Machine_Learning]]

# Introduction
L2 (Ridge) Regularization is a type of regularization ([[Regularization|link]]) where we add penalty proportional to the square of the size of model's parameters:
$$
Loss_{reg}(\theta) = Loss(\theta) + \lambda \lVert \theta \rVert_2^2
$$
where:
- $\theta = (\theta_1, \ldots, \theta_n)$ - Model's parameters
- $\lVert \theta \rVert_2^2 = \sum_{i=1}^n \theta_i^2$ 
- $\lambda \ge 0$ - Regularization strength (chosen parameter)

It makes the model to have smaller parameters what prevents relying too much on a single feature based on which we make predictions ([[Dataset of observations of random variables X, Y - Variables per sample, feature and target variable|link]]).

Unlike L1 regularization ([[L2 Regularization (Ridge)|link]]), it doesn't have a tendency to produce sparse models, that is models with a small number of parameters, by reducing some of the parameters to zero.

When we have two correlated features, L2 usually makes parameters corresponding them similar, what causes that both features has a similar impact on a prediction.
# Derivation
When training models, we minimize the loss using derivatives (e.g., gradient descent) ([[Gradient Descent - ML|link]]). 

We update parameters in iterations, by subtracting from them a value relative to the derivative of a loss function in each iteration.

Derivative of a loss with L2 regularization is:
$$
\frac{\partial Loss_{reg}}{\partial \theta_j} = \frac{\partial Loss}{\partial \theta_j} + \frac{\partial}{\partial \theta_j} \lambda \theta^2_j =
\frac{\partial Loss}{\partial \theta_j} + 2\lambda \theta_j
$$
Normally in gradient descent, as a new value for the parameter $\theta_j$ we use this value:
$$
\theta_j^{new} = \theta_j - \eta \frac{\partial Loss}{\partial \theta_j}
$$
And with regularization that becomes:
$$
\begin{align}
 & \theta_j^{new} = \theta_j - \eta (\frac{\partial Loss}{\partial \theta_j} + 2\lambda \theta_j) \\
 & \theta_j^{new} = (1 - 2\eta\lambda) \theta_j - \eta \frac{\partial Loss}{\partial \theta_j}
\end{align}
$$
So each time we shrink parameter $\theta_j$ by a factor $(1 - 2\eta\lambda) < 1$.

That's why L2 regularization is also called:
- Weight decay
- or Shrinkage estimator

Unlike the L1 regularization, L2 doesn't tend to produce sparse models.

That's because, as $\theta_j$ is getting close to zero, the value $(1 - 2\eta\lambda) \theta_j$ is also getting closer to zero, so we are changing a value of the parameter by less and less. 
# Geometric interpretation
L2 regularization adds a penalty:
$$
\lambda \lVert \theta \rVert_2^2 = \lambda(\theta_1^2 + \ldots + \theta_n^2)
$$
Finding a minimum of a loss with a penalty:
$$
\min_\theta Loss(\theta) + \lambda \lVert \theta \rVert_2^2
$$
is equivalent to finding a minimum of a loss with a constraint:
$$
\min_\theta Loss(\theta) \text{, where } \lVert \theta \rVert_2^2 \le c
$$
for some value $c$.

Set of parameters satisfying the constraint $\lVert \theta \rVert_2^2 \le c$  is a n-dimensional ball if $\theta = (\theta_1, \ldots, \theta_n)$ is n-dimensional. So we are looking for a minimum of the loss function, only considering parameters $\theta$ which are contained in that ball.

The $c$ value is only hypothetical, we don't know it's value.

Once we find the minimum of the loss with a penalty: 
$$
\min_\theta Loss(\theta) + \lambda \lVert \theta \rVert_2^2
$$
that gives us parameters $\theta$ which forms the sphere $\lVert \theta \rVert_2^2 = c$ for some value $c$ which touches the loss function curve.

So before finding a minimum of the loss function with a penalty, value $c$ is only hypothetical, we don't know its value. We can only calculate it after finding the minimum of the loss function with a penalty.

Value $c$ depends on the value of $\lambda$. For smaller values of $\lambda$, we receive a bigger value $c$ because the penalty $\lambda \lVert \theta \rVert_2^2$ is small so it doesn't affect too much where is the minimum of the Loss.
# Properties
Below are described properties of L2 regularization.
## No sparsity
L2 doesn't have a tendency to create sparse models, that is models with a small number of parameters, by setting value of some parameters to zero.

That's because derivative of the penalty $\lambda \theta_i^2$ is $2\lambda \theta_i$, so it is relative to a value of $\theta_i$. 

When a value of the parameter $\theta_i$ is getting closer to zero, the value by which we are updating the parameter $(1 - 2\eta\lambda) \theta_i$ is also getting closer to zero, so we are making smaller and smaller updates, so it is difficult to reduce $\theta_i$ to the exact zero.
## Continuous loss (differentiable)
The penalty function $\lambda \theta_i^2$ is continuous so we can easily calculate a derivative.
## It favors making parameters similar for correlated features
If we have correlated features, then with L2 regularization we will more likely obtain similar parameters for those features, rather than reducing one parameter to zero

 hat's because the penalty is bigger for a single, big parameter, than for two smaller parameters, for example:
- $\theta_1 = 0 \wedge \theta_2 = 3 \implies \text{penalty} = 0 + 9 = 9$ 
- $\theta_1 = 1.5 \wedge \theta_2 = 1.5 \implies \text{penalty} = 2.25 + 2.25 = 4.5$ 
## Small gradients
For two correlated features, L2 makes parameters corresponding to both features small like described in the previous section.

That causes gradients to be small and with small gradients, updating parameters is stable because we update values of parameters by a little. 

If we update parameters by a lot, then we might miss the optimal value. For example we update a parameter from 2 to 6 while the optimum was 3.
## For linear models we get unique solution
- That is for models which can be written as $f_\theta(x) = \sum_{i=1}^n \theta_1 \phi_1(x)$ where $\phi$ is a function performing transformations on $x$ 
# Relation to MAP estimation


#MachineLearning 