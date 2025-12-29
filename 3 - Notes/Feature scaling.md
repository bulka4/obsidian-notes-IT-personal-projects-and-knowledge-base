Tags: [[__Machine_Learning]]

# Introduction
Feature scaling is a process of transforming input variables for a model so that they are on a similar range or distribution. 

It ensures that features contribute proportionally to the model, especially for algorithms that rely on distances (like KNN ([[K nearest neighbors (KNN)|link]]), clustering ([[Clustering|link]])) or gradients (gradient descent ([[Gradient Descent - ML|link]])).

Without scaling, if a model relies on distances or gradients, features with small numeric ranges are dominated by those with large ranges and they contribute much less to the value of the loss function during training a model.

That causes, that a model relies more on features with high values when making predictions.
# Common scaling methods
- Min-Max scaling (Normalization) - [[Min-Max scaling (Normalization)|link]]
- Standarization - [[Standarization|link]]

#MachineLearning  