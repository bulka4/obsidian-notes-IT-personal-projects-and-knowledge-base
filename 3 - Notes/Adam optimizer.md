Tags: [[__Machine_Learning]]

# Introduction
Adam optimizer works similar like gradient descent ([[Gradient Descent - ML|link]]), it just uses a different formula for updating parameters.

Let's assume, that we have:
- $\large \theta_t$ - Model parameters at step $t$ 
- $\large g_t = \nabla_\theta L(\theta_t)$ - Gradient of a loss function w.r.t. model parameters $\theta$ 

First we calculate so called the first moment state $\large m_t$ and second moment state $\large v_t$ :
$$
\large \begin{align}
& m_t = \beta_1 m_{t-1} + (1-\beta_1)g_t \\
& v_t = \beta_2 v_{t-1} + (1-\beta_2)g_t^2
\end{align}
$$
whereL
- $g_t^2$ is elementwise square (every element of the matrix $g_t$ is squared)
- $\beta_1, \beta_2$ - Chosen values, so called decay constants

Then, we calculate so called bias-corrected moments:
$$
\large \begin{align}
& \hat{m_t} = \frac{m_t}{1-\beta_1^t} \\ 
& \hat{v_t} = \frac{v_t}{1-\beta_2^t} \\ 
\end{align}
$$
and update model parameters:
$$
\large
\theta_{t+1} = \theta_t - \alpha \frac{\hat{m_t}}{\sqrt{\hat{v_t}} + \epsilon}
$$
where:
- $\alpha$ - Learning rate
- $\epsilon$ - Small, constant value for stability (so we don't divide by zero)

#MachineLearning 