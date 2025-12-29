Tags: [[__Machine_Learning]]

# Introduction
Confusion Matrix tells us how many times a model predicted class X while the true class was Y, where X and Y belongs to a set of available classes.

For a binary classification, it looks like this:
$$
\begin{array}{c|c|c|c} 
 & \text{Predicted Positive} & \text{Predicted Negative} \\ \hline
\text{Actual Positive} & \text{True Positive (TP)} & \text{False Negative (FN)} \\
\text{Actual Negative} & \text{False Positive (FP)} & \text{True Negative (TN)}
\end{array}
$$
So for example, True Positive value indicates how many times model predicted the Positive class while the true class was also Positive.

If we have more than two classes then it looks like this:
$$
\begin{array}{c|c|c|c} 
 & \text{Predicted Class 1} & \text{Predicted Class 2} & \text{Predicted Class 3} \\ \hline
\text{Actual Class 1} & 1 & 2 & 3 \\
\text{Actual Class 2} & 4 & 5 & 6 \\
\text{Actual Class 3} & 7 & 8 & 9
\end{array}
$$

#MachineLearning 