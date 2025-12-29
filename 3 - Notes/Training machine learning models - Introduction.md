Tags: [[__Machine_Learning]]

# Introduction
By training a machine learning model ([[What is a Machine Learning model|link]]), we mean finding parameters for that model for which the performance of the model, according to chosen criteria, is the best.

We train a model using a dataset with features and target variables ([[Features and target variables|link]]):
$$
\large 
D = \{(x_1, y_1), \dots, (x_n, y_n)\} = \{(x_i, y_i)\}_{i=1}^n
$$
Model takes as an input a feature $\large x_i$ and based on that, tries to predict the value of the target variable $\large y_i$ . 

We always split the model into a training and testing dataset ([[Train - test split of a dataset|link]]) and we use the training dataset to train the model, and use the testing dataset to evaluate the model ([[Evaluating ML models|link]]).

Training is often done by minimalizing a loss function ([[Loss functions|link]]).

#MachineLearning 