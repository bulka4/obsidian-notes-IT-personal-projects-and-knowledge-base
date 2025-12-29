Tags: [[__Machine_Learning]]

# Introduction
Dimensionality reduction is an operation of reducing amount of features we use to make predictions using a machine learning model.

It helps to:
- Remove noise (irrelevant features)
- Improve model performance:
	- Reduced overfitting
	- Some models (like KNN and clustering) perform worse with many features
- Speed up training

There are two main types of techniques for dimensionality reduction:
- Feature extraction
- Feature selection
# Feature extraction
Feature extraction techniques create new features from the original ones, merge many correlated features into new ones.
- PCA (Principal Component Analysis) - [[PCA (Principal Component Analysis)|link]]
- t-SNE
- Autoencoders - [[Autoencoders - Dimensionality reduction|link]]
# Feature selection
Feature selection techniques selects a subset of the most relevant features.
- Variance threshold - [[Feature selection with a variance threshold|link]]
- Correlation analysis - [[Pearson Correlation - Dimensionality reduction|link]]
- Mutual information - [[Mutual information - Dimensionality reduction|link]]
- LASSO (L1 regularization)
- Tree-based feature importance - [[Decision Tree - Dimensionality reduction|link]]

#MachineLearning 