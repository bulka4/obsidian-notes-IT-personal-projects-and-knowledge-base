Tags: [[__Machine_Learning]]

# Introduction
Recall answers the question:

*When the real category was positive, in how many percent of cases model was correct?*

or:

*Out of all the actual positive, how many of the did the model catch?*

It is good metric when we want to detect as many positives as possible, for example in case when we are detecting a disease. If someone is sick but we predict that they are healthy - that is a big problem.

It is calculated using values from a Confusion Matrix ([[Confusion matrix|link]]):
$$
\text{Recall} = \frac{TP}{TP + FN} = \frac{TP}{\text{total number of positive samples}}
$$

#MachineLearning 