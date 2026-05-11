Tags: [[__Machine_Learning]]

# Introduction
Class Weights / Cost-Sensitive Learning is an algorithm-level method for training ML models for classification on an imbalanced dataset ([[Training classification models on an imbalanced dataset|link]]).

In this method, we assign weights to different classes what causes that predictions for those classes has bigger or lower impact on the loss function (higher weight = higher impact).

When there is a higher loss for a class, the model is more likely to make correct predictions for this class.

We can use it in case of training on an imbalanced dataset by assigning higher weights to the minority class.
# How it works
***1. Assign weights to classes***
Assign higher weight to the minority class and lower to the majority one.

***2. Modify the loss function***
Modify the loss function using assigned weights, for example in case of Cross-Entropy ([[Cross-Entropy for classification|link]]):
$$
\large
\text{Loss} = - \frac{1}{n} \sum_{i=1}^n w_{Y_i} \log(p_{Y_i \mid X_i}(y_i \mid x_i; \theta))
$$
where:
- $\large p_{Y_i \mid X_i}(y_i \mid x_i; \theta)$ - Predicted probability of the class $y_i$ 
- $\large w_{Y_i}$ - Weight assigned to the true class

Weights causes, that wrong predictions for the minority class has bigger impact on value of the loss, so when training the model and minimizing the loss, it is more likely to obtain correct predictions for the minority class.
# Comparison to a focal loss
Compared to a focal loss ([[Focal loss|link]]):
- In this method we can assign higher or lower weights to any class to make a model to focus more on making correct predictions for this class
- While when using a focal loss, we make the model to focus more on making correct predictions just on samples for which probability is small. We can't choose which samples to focus.

#MachineLearning 