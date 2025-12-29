Tags: [[__Machine_Learning]]

# Introduction
Standarization is a technique of feature scaling ([[Feature scaling|link]]).

It rescales features to have mean 0 and standard deviation 1:
$$
x' = \frac{x - \mu}{\sigma}
$$
where:
- $\mu$ - Mean
- $\sigma$ - Standard deviation
# Properties
- Handles outliers better than Min-Max in many cases.
- Often preferred for distance-based models (KNN, SVM) or models using gradient descent (NNs, linear/logistic regression).

#MachineLearning 