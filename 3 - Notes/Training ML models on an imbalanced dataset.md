Tags: [[__Machine_Learning]]

# Recollection
Let's remind, that:
- For training ML models we use a dataset $\large D = \{(x_i, y_i)\}_{i=1}^n$ (more information here - [[Features and target variables|link]]), where:
  - $x_i$ - Feature vector for the $i$-th data sample
  - $y_i$ - Target variable for the $i$-th data sample
- We can visualize feature vectors in a feature space in common scenarios like illustrated here - [[Feature space visualization|link]].
# Introduction
An imbalanced dataset is one where we have significantly different number of data samples for different values of the target variable. That target variable can be both continuous or discrete ([[Types of variables used for creating ML models|link]]).

That causes problems when training machine learning models ([[Training machine learning models - Introduction|link]]) for classification and regression ([[Applications of ML models - overview|link]]) because when model makes wrong predictions for data samples with rare values of the target variable, it doesn't have a significant impact on the value of the loss function ([[Loss functions|link]]), so minimizing the loss doesn't make the model to make accurate predictions for those rare cases.

For example, if in our dataset we have 1000 samples which belongs to the class A and 10 samples which belongs to the class B, model can always predict A and loss will be small.

Or when we have 1000 samples with value of the target variable $Y$ between 10-15, and 10 samples where $Y$ is between 25-30, model will be always predicting values between 10-15 and loss will be small.

There are separate methods for models for classification and regression:
- [[Training classification models on an imbalanced dataset]]
- [[Training regression models on an imbalanced dataset]]
# Related topics
Related topics needed to understand this topic:
- [[Types of variables used for creating ML models]]
- [[Training machine learning models - Introduction]]
- [[Loss functions]]
- [[Classification models]]
- [[Regression models]]
- [[Feature space]]
- [[Feature space visualization]]

#MachineLearning 