Tags: [[__Machine_Learning]]

# Introduction
**Bias** measures how far are model's predictions from the true values on average.

**Variance** measures sensitivity of the model to changes in the training dataset ([[Train - test split of a dataset|link]]). High variance means that model's predictions would change a lot if we make small changes in the training dataset.

Usually, values of bias and variance mean the following:
- High bias means that the model is too simple as is not able to capture the true relation between features and target variable. So it performs poorly on both training and testing datasets.
- High variance means that the model is too complex and we observe overfitting, that is model performs very well on the training dataset, but very poorly on new data samples which it didn't see before

Those are only conceptual values, we can't calculate them because they describe how model would behave on all the possible data which we don't have access to.

#MachineLearning 