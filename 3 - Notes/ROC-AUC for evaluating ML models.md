Tags: [[__Machine_Learning]]
#MachineLearning 

# ROC graph
## Introduction
The ROC graph helps us to choose the best decision threshold ([[Decision - classification threshold|link]]) for classification models ([[Classification models|link]]) for a binary classification. 

It shows us what are the True Positive Rate and False Positive Rate (TPR and FPR) values for different thresholds. 

- We want to maximize the TPR and minimize the FPR. 
- Usually increasing TPR also increases FPR.
- For good models, changing a threshold can increase TPR a lot and increase FPR only slightly
- For the perfect model we can choose such a threshold that TPR = 1 (max) and FPR = 0 (min)
	- The perfect model is the one which assigns higher scores (probabilities) to every positive sample than to every negative sample. More information about it is below in the "Perfect model" section.
## True and False Positive Rate (TPR and FPR)
In order to create a ROC graph we are calculating two values, a True and False Positive Rate (TPR and FPR) for different decision thresholds:
$$
\text{True Positive Rate} = 
\frac{\text{true positives}}{\text{true positives} + \text{false negatives}}
= \frac{\text{true positives}}{\text{total number of positives}}
$$
$$
\text{False Positive Rate} 
= \frac{\text{false positives}}{\text{false positives} + \text{true negatives}}
= \frac{\text{false positives}}{\text{total number of negatives}}
$$

We are choosing such a decision threshold which:
- Maximizes the True Positive Rate
- Minimizes the False Positive Rate

In the ROC graph, we show TPR and FPR values for different decision thresholds:
- FPR on the x axis
- TPR on the y axis

It looks like this:
![[2 - Images/ROC-AUC for ML models/Screenshot 1.png]]
## OK model

## Perfect model
The perfect model here means a model which assigns higher scores (probabilities) to every positive sample than to every negative sample. 

Then, there are thresholds for which we get:
- TPR = 0 and FPR = 0
- TPR = 1 and FPR = 0 (100% accuracy)
- TPR = 1 and FPR = 1
### Example
For example, a perfect model might assign scores (probabilities) to data samples like that:
```
0.99  Positive
0.95  Positive
0.90  Positive
0.20  Negative
0.10  Negative
0.05  Negative
```

Then:
- For threshold = 1
	- No sample is predicted as positive
	- TPR = 0, FPR = 0
- For threshold = 0.9
	- All the positive samples are classified as positive
	- TPR = 1, FPR = 0
- For threshold = 0
	- All samples are classified as positive
	- TPR = 0, FPR = 1
# AUC
AUC is an area under a ROC graph. The higher value the better. 
- The AUC = 1 indicates a perfect model
- AUC = 0.5 indicates random guessing (50% accuracy)
- AUC = 0 indicates 0% accuracy (always wrong predictions)
