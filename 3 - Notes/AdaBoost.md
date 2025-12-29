Tags: [[__Machine_Learning]]

# Introduction
AdaBoost (short for Adaptive Boosting) is a model which can be used for both classification and regression tasks.

The original version is only for a binary classification and that use case is explained in more detail in this document.

AdaBoost is an ensemble learning algorithm that combines many weak learners (models, typically shallow decision trees, often called stumps) into a single strong model.
# Links
How this model works is very well explained in this video: [youtube - StatQuest](https://www.youtube.com/watch?v=LsK-xG1cLYA)
# Training process
## High level
Here is how it works on a high level:

***1. Train a weak learner*** 
Train a single, simple model, like a small decision tree

***2. Evaluate* its errors**
Find which samples were misclassified.

***3. Increase* the weights** 
Increase weights of the misclassified samples, so the next learner focuses on them.

Weights are assigned to data samples and they are used during training. Higher weights causes that the loss is higher for wrong predictions.

***4. Train* another weak learner** 
Train another learner using updated weights.

Repeat this process several time to create multiple learners (models). This way, each new model focuses more on the “harder” examples that earlier models got wrong.
## Annotations
As mentioned in the section explaining the training process on a high level, we train multiple learners, each one in a different iteration.

The lower index $t$ indicates an iteration number. In this document we use the following annotations:
- $h_t(x_i)$ - Output of the learner for the i-th data sample created in the t-th iteration
- $w_i^{(t)}$ - Weight for the i-th data sample in the t-th iteration
- $y_i$ - Value of the target variable in the i-th data sample
## Details
### Calculating weights
Weights assigned to data samples, at the beginning are all equal to $1 / N$ where $N$ is a total number of samples.

After training a learner, we compute its weighted error:
$$
\epsilon_t = \frac{\sum_{i=1}^{N} w_i^{(t)} 1[h_t(x_i) \neq y_i]} {\sum_{i=1}^{N} w_i^{(t)}}
$$
Then we assign a learner's weight using this formula:
$$
\alpha_t = \frac{1}{2}\ln( \frac{1 - \epsilon_t} {\epsilon_t} )
$$
- If the weak learner is perfect $(\epsilon_t = 0)$ , then $\alpha_t \to \infty$  
- If it’s random $(\epsilon_t = 0.5)$, then $\alpha_t = 0$
- If it's worse than random $(\epsilon_t < 0.5)$, then $\alpha_t < 0$
- So, the better the learner, the more influence it gets

Then we update weights of training samples using this formula:
$$
w_i^{(t+1)} = w_i^{(t)} * exp(-\alpha_t y_i h_t(x_i))
$$
So:
- If the sample was classified correctly ($y_i = h_t(x_i)$), then weight decreases: $-\alpha_t * (+1) = -\alpha_t$
- Otherwise ($y_i \neq h_t(x_i)$) weight increases: $-\alpha_t * (-1) = \alpha_t$

Sample weights are normalized so their total sum equal to 1:
$$
w_i^{(t+1)} = \frac{ w_i^{(t+1)} } { \sum_{j=1}^{N} w_j^{(t+1)} }
$$
### Resampling training dataset
After training one learner, we are resampling our dataset in order to train the next learner.

We start with calculating a cumulative sum of our sample weights (sum of weights from all the records up until a given record):
$$
\begin{array}{c|c|c}
\text{Sample number} & \text{weight} & \text{cumulative sum} \\ \hline
1 & 0.10 & 0.10 \\
2 & 0.20 & 0.30 \\
3 & 0.10 & 0.40 \\
4 & 0.50 & 0.90 \\
5 & 0.10 & 1 \\
\end{array}
$$

then we choose a random number $r$ between 0 and 1 and pick that sample for which has the smallest cumulative sum bigger than $r$.

For example if we choose $r = 0.8$, that means that $0.4 < 0.8 < 0.9$ so we choose the sample nr 4.

We repeat this process $N$ times to obtain a dataset of the same size as the previous one. 

Here is a few important facts:
- Samples with higher weight are more likely to be chosen
- Some samples might be duplicated, some might not appear in the new dataset
# Making predictions
Making predictions for a binary classification is done by combining all learners’ predictions via weighted voting.

Each learner predicts one of two labels which represents votes (true of false):$$
h_t(x) \in \{-1, 1\}
$$ Prediction $h_t(x) = -1$ indicates one class (false), and $h_t(x) = 1$ indicates the second one (true).

To make the final prediction, we take a weighted sum of all the learner's votes:
$$
F(x) = \sum_t\alpha_th_t(x)
$$
Where weights $\alpha_t$ are calculated based on the learner's performance on all the data samples. Better learners has higher weights and because of that their votes are more important.

And the final prediction is:
$$
H(x) = sign(F(x)) = 
\begin{cases}
+1, & \text{if } x > 0, \\
0, & \text{if } x = 0, \\
-1, & \text{if } x < 0
\end{cases}
$$
If $H(x)$ = 0, then we need to decide whether it means the true or false class.