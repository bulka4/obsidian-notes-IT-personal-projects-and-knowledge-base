Tags: [[__Machine_Learning]], [[_Mathematical_analysis]], [[__Mathematics]]

# Introduction
When we train a machine learning model, we often do this by minimizing a loss function value using an optimization algorithm (e.g. gradient descent ([[Gradient Descent - ML|link]]) or Adam) which uses gradients of that loss function.

If gradients of a loss function are super small or super big, then optimization algorithms using gradients has a problem, because they change values of model parameters by too little or too much.

This is typically the case, when our model is a composition of multiple functions (like in neural networks), and to calculate a gradient of the loss, we need to multiply all those functions and:
- When gradient for each function is smaller than 1 - gradient of loss is super small
- When gradient for each function is greater than 1 - gradient of loss is super big

#MachineLearning #MathematicalAnalysis #Mathematics 