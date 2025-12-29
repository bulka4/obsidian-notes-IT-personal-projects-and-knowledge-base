Tags: [[__Machine_Learning]]

# Introduction
Balanced Random Forest is a version of the standard Random Forest ([[Random Forest|link]]).

It is an example of a Balanced Ensemble Method used to train machine learning model for classification on an imbalanced dataset ([[Training classification models on an imbalanced dataset|link]]).

It creates multiple decision trees, where each tree is trained on a balanced dataset, which is a subset of the original dataset.
# How it works
For each tree in the forest:
- Select all the samples which belong to the minority class
- Randomly select samples which belong to the majority class
	- Pick a similar number of samples as for the minority class
- Train the tree on this balanced dataset

Predictions are done like in the standard Random Forest model, that is all the trees make predictions (vote), and we choose the most popular prediction (vote).

#MachineLearning 