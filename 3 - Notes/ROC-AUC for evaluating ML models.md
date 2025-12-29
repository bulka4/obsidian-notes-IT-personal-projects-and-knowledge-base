Tags: [[__Machine_Learning]]

# Introduction
### ROC graph
This graph helps us to choose the best decision threshold for classification models. 

In order to create a ROC graph we are calculating two values, a True and False Positive Rate for different decision thresholds:
$$
\text{True Positive Rate} = \frac{\text{true positives}}{\text{true positives} + \text{false negatives}}
$$
$$
\text{False Positive Rate} = \frac{\text{false positives}}{\text{false positives} + \text{true negatives}}
$$
We can also write:
$$
\text{True Positive Rate} = \frac{\text{true positives}}{\text{total number of positives}}
$$
$$
\text{False Positive Rate} = \frac{\text{false positives}}{\text{total number of positives}}
$$
We are choosing such a decision threshold which:
- Maximizes the True Positive Rate
- Minimizes the False Positive Rate

In the ROC graph, we show:
- False Positive Rate on the x axis
- True Positive Rate on the y axis

It looks like this:
![[2 - Images/ROC-AUC for ML models/Screenshot 1.png]]
### AUC
AUC is an area under a ROC graph. The higher value the better. 
- The AUC = 1 indicates a perfect model
- AUC = 0.5 indicates random guessing (50% accuracy)
- AUC = 0 indicates 0% accuracy (always wrong predictions)

#MachineLearning 