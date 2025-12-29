Tags: [[__Machine_Learning]]

# Introduction
Precision answers the question:

*Out of all the items that model predicted as positive, how many of them were actually positive (model was correct)?*

It is useful metric when we want to be sure that when model predicts a positive, it is a positive indeed. For example when we predict that a client will be interested in a marketing campaign but in reality they are not, we will waste time contacting them.

It is calculated using values from a Confusion Matrix ([[Confusion matrix|link]]):
$$
\text{Precision} = \frac{TP}{TP + FP} = \frac{TP}{\text{total number of samples predictes as positive}}
$$

#MachineLearning 