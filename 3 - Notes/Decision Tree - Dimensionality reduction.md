Tags: [[__Machine_Learning]]

# Introduction
Decision tree ([[Decision Tree|link]]) can be used for a dimensionality reduction ([[Dimensionality reduction|link]]), that is reducing number of features we use for making predictions.

As explained in the document about a decision tree ([[Decision Tree|link]]), it calculates a gini impurity for each feature measuring how useful is that feature for making predictions.

We can reduce number of features, by choosing those features, which have the lowest gini impurity value, those are feature higher in the tree structure.
# Problem
This technique might be sometime misleading because it favors continuous and high-cardinality categorical variables.

That's because for such variables there is more different conditions to split a dataset.

 When we generate more different split datasets, there is a higher chance that some of those datasets will be better for making predictions (it will be easier to make predictions for samples from it) than datasets produced by splitting using a different feature which produces less split datasets.

#MachineLearning 