Tags: [[__Machine_Learning]]
#MachineLearning 

# Introduction
A recall is primarily used for a binary classification but can be also used for a multi-class classification.

It answers the question:
>How many percent of positive samples were correctly detected by a model?

or
>When the real category was positive, in how many percent of cases model was correct?

It is good metric, for example in case when we are detecting a disease. If someone is sick but we predict that they are healthy - that is a big problem.

It is calculated using values from a Confusion Matrix ([[Confusion matrix|link]]):
$$
\text{Recall} = \frac{TP}{TP + FN} = \frac{TP}{\text{total number of positive samples}}
$$

#MachineLearning 