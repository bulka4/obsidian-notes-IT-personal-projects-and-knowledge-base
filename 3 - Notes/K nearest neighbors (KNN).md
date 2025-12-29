Tags: [[__Machine_Learning]]

# Introduction
K nearest neighbors (KNN) is a model for classification and regression.

On a high level, making predictions for a new data point is done in the following way:
- Find data points from a training dataset which are the most similar to this new point
- As a prediction we take the most common class / average value among the found, most similar data points
# How KNN works
In order to use KNN we need to:
- Store the training data - There is no training phase, we just keep the dataset in memory
- Choose k - This is a number of neighbors we will consider

When a new data point appears, then in order to make predictions we follow the steps:
- **Compute a distance** - Between the new data point and all the other points in the training dataset (For more info about calculating distance between vectors, refer [[Distance between vectors|here]])
- **Find k nearest neighbors** - Find the k points from the training dataset closest to the new point
- **Make the prediction** 
	- **Classification** - Assign to a new point the most common class among the found k nearest neighbors
	- **Regression** - As a prediction we take average of k nearest neighbors' target values 
# KNN with weighted distance metric
Interesting article: https://dergipark.org.tr/tr/download/article-file/904927

Instead of using Euclidean metric we can use metric which measures distance between datapoints using weight for each attribute, so this metric might looks like this:
$$
Dist(x_1, x_2) = \sqrt{w_1 * (x_{11} - x_{21}) + ... + w_n * (x_{1n} - x_{2n})}
$$
or
$$
Dist(x_1, x_2) = \sqrt{f(w_1 * (x_{11} - x_{21}) + b_1) + ... + f(w_n * (x_{1n} - x_{2n}) + bn)}
$$
where f is an activation function like in neural networks and $b_i$ are biases.

Weights $w_i$ and biases $b_i$ might be learnt by model like in neural networks.
# Cons
## Doesn't perform well in high-dimensional datasets
If dataset is high-dimensional (a lot of features $x_i$), then distance between feature vectors become less meaningful.

#MachineLearning 