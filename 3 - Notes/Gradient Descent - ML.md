Tags: [[__Machine_Learning]], [[_Mathematical_analysis]], [[__Mathematics]]

# Introduction
Gradient descent is an optimization algorithm used to find a minimum of a function.

In context of ML, it helps us to find the parameters (weights) of a model ([[What is a Machine Learning model|link]]) that minimize a loss function ([[Loss functions|link]]) (like Mean Squared Error in linear regression, or Cross-Entropy in classification).

It’s how many models learn — they adjust their parameters little by little in the direction that makes predictions more accurate.

It calculates gradients of a loss function with respect to model's parameters in order to determine how to change model's parameters to cause the loss (value of the loss function) smaller.
# Algorithm for updating model's parameters
Let's say our model has parameters $\theta$ (for example weights in a linear regression) and we have a loss function $J(\theta)$. The gradient descent update rule is:
$$
\theta = \theta - \eta * \nabla_\theta J(\theta)
$$
where:
- $\eta$ - Learning rate (step size) - value we need to choose
- $\nabla_\theta J(\theta)$ - Gradient (vector of partial derivatives of the loss with respect to each parameter)

So at each iteration, we:
1. Compute the gradient of the loss function with respect to the parameters.
2. Move the parameters a bit so value of the loss function becomes smaller for the training dataset.

We perform those iterations until one of conditions is satisfied:
- The loss improvement is very small (converged)
- We’ve reached a maximum number of iterations
- The gradient magnitude is near zero
# Why to use derivatives
Derivate with respect to a specific parameter of a function, tell us if that function (loss in this case) is increasing or decreasing when we increase value of that parameter. If derivative is positive, that means that function values increases when increasing value of that parameter.

For example, in the function below we can see, that in the point $x = 2$ derivative is positive, because increasing value of x will cause the function to increase its value:
![[2 - Images/Gradient Descent/Screenshot 1.png]]

So when we subtract derivative from the parameter, it causes function to decrease for that parameter.
# Role of the learning step
With bigger learning step, we might reach the minimum of the loss faster because we are changing parameters more at each step. 

But there is also higher risk that we will miss that minimum because we might change parameters too much. For example in one iteration we have a parameter value = 0.5, then in the next iteration we change it to 0.7, while the loss minimum was for 0.6.

Gradients only tells us whether loss value will increase or decrease after increasing a parameter, but it doesn't tell us how much do we need to change that parameter to reach the minimum.
# Local minimum problem
Gradient descent method might cause that we find a local minimum instead of the global one. 

For example, if we have a function like shown above in the 'Why to use derivatives' section, and we start gradient descent algorithm at $x=-3$, then that algorithm will be increasing value of x, since that will be causing value of the function to decrease.

But once we reach $x \approx -1$, then no matter if we increase or decrease $x$, it will result in a higher value of the function, so algorithm will finish there.

That algorithm doesn't know that if we keep increasing $x$, then function will start decreasing again for $x > 2.5$.

But if we start the algorithm with the initial $x=3$, then algorithm will continue increasing $x$ as that will result in smaller values of the function.

That's why the initial value of $x$ is important.
# Vanishing / exploding gradient problem
When using gradient descent, we might encounter a problem with vanishing / exploding gradients like described here - [[Vanishing - exploding gradients]].

#MachineLearning #MathematicalAnalysis #Mathematics 