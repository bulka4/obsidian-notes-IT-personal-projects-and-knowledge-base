Tags: [[__Machine_Learning]]

# Introduction
Random forest is a model for classification, regression and clustering. It is good when our dataset is imbalanced.

It is based on the decision tree model ([[Decision Tree|link]]). It builds multiple decision trees, where each tree is built differently because each tree is built using a dataset which is a random modification of the main dataset.

Then all the trees are used together to make predictions. This helps with generalization of models, to prevent overfitting.

Also, random forest can be used to calculate feature importance scores, which tell us how useful each feature is for making predictions.
# Benefits
Random forest helps with issues we have with a decision tree:
- Tendency to overfitting
- High variance - small changes in the training dataset can produce very different trees

Plus it has the same benefits as a decision tree:
- Interpretability - We can see what conditions are used to make predictions. Although interpretability is harder than in case of a single decision tree as here a prediction is done using multiple trees.
- We don't assume here a linear relationship between the target variable and features, and independency between data samples
- Handles a mix of continuous and discrete features
- Don't require preprocessing, e.g. scaling, normalization, standardization
- Works for both classification and regression
# Drawbacks
Like a decision tree:
- Can struggle with extrapolation ([[Machine Learning - Extrapolation|link]])
- It favors continuous and high-cardinality categorical variables what can be misleading when we interpret importance of features
	- That's because for such variables there is more different conditions to split a dataset.
	- When we generate more different split datasets, there is a higher chance that some of those datasets will be better for making predictions (it will be easier to make a prediction for a sample which we select from it) than datasets produced by splitting using a different feature which produces less split datasets.

Additionally, it is:
- Slower an requires more memory than a single decision tree. Compared to other models, the speed and memory usage is medium.
- It is reducing variance but not bias - If all decision trees are wrong, then averaging a result won't help
# Building Random Forest
It builds multiple decision trees where each tree is built differently because we use two techniques which ensures randomness in building trees:
- Bootstrapping (Bagging)
- Random feature selection
## Bootstrapping (Bagging)
Bootstrapping works in the following way:
- For each tree, we select a randomly samples from the dataset which will be used for training.
- In a dataset for one tree, some rows might appear multiple times, and some might not appear at all.
- Total number of samples stay the same.
- Thanks to that, each tree is built using different dataset.

Around 1/3 of original samples are not used for training a given tree, those are so called Out-of-Bag samples and they can be used to estimate model's performance.
## Random feature selection
When splitting a node, instead of considering all the features from the dataset, we select randomly a subset of features.

We do this because, when some features are very strong predictors (it is relatively easy to make predictions based on them), then all the trees might rely on those features and give similar predictions (so trees will be correlated).

Typically we use the following number of features:
- For classification: $\sqrt{d}$  
- For regression: $d / 3$ 
where $d$ is the total number of features 

It helps preventing overfitting in a high-dimensional datasets.
# Making predictions
Predictions are made in the following way:
- Classification: Each tree votes for a class, and as the final prediction we choose the class with the most votes
- Regression: Each tree predicts a value, and as the final prediction we take an average of those predictions
# Feature importance scores
Random forest can be used to calculate scores representing how important are different features for making predictions.

It is calculated in the following way:
- Measure how much impurity (Gini or variance) decreases every time a feature is used to split a node
- Sum up this decrease across all trees for each feature 
- Normalize the sum
# Clustering
Random forest can be also used for clustering. Here's how to do this:
- For each data sample pair, we count how many times that pair was assigned to the same leaf by different trees.
- More times a pair was assigned to the same leaf by different trees, the more similar those samples are (so they should be in the same cluster)

We create a matrix:
$$
A = \begin{pmatrix}
a_{11} & \dots & a_{1n} \\
\vdots & \ddots & \vdots \\
a_{n1} & \dots & a_{nn} \\
\end{pmatrix}
$$
where:
- $n$ - Number of samples in the dataset
- Each row and column correspond to one sample (the $i$-th row and $i$-th column correspond to the same sample)
- $a_{ij}$ indicates how many trees assigned samples $i$ and $j$ to the same leaf

Samples assigned to the same leaf by a tree are similar to each other as described in the document about decision trees - [[Decision Tree|link]].

So values $a_{ij}$ indicate how similar samples $i$ and $j$ are. Similar samples will be assigned to the same cluster.
# Balanced Random Forest (for imbalanced data)
We can use a Random Forest model when our training dataset is imbalanced. We split then our dataset into multiple balanced datasets and train a separate decision tree on each new dataset.

More information is here - [[Balanced Random Forest|link]].

#MachineLearning 