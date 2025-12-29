Tags: [[__Machine_Learning]]

# Introduction
Focal loss is an algorithm-level method for training ML models, especially neural networks, for classification on an imbalanced dataset ([[Training classification models on an imbalanced dataset|link]]).
# How it works
It is extension of the standard Cross-Entropy formula ([[Cross-Entropy for classification|link]]):
$$
\large
CE = - \frac{1}{n} \sum_{i=1}^n \log(p_{Y_i \mid X_i}(y_i \mid x_i; \theta))
$$
Focal loss is defined as:
$$
\large
FL(p_t) = -\sum_{c=1}^C \alpha_c (1-p_c)^\gamma y_c \log(p_c)
$$
where:
- $C$ - Number of classes
- $y_c \in \{0, 1\}$ - Is 1 if the true class is $c$, otherwise 0
- $p_c$ - Predicted probability of for the class $c$ 
- $\alpha_c$ - Optional class weight
- $\gamma \ge 0$ - Focusing parameter (chosen by us)

Interpretation:
- When $p_c \approx 1$, then $(1-p_c)^\gamma \approx 0$, so the loss value is reduced
- When $p_c \approx 0$, then $(1-p_c)^\gamma \approx 1$, so the loss value remains high

This makes the model to focus more on samples which belongs to the minority class, since model's usually predicts for them smaller probabilities.

Optional parameters $\alpha_c$ is chosen by us and gives us more control over how important are different classes, to which classes model should pay more attention.

#MachineLearning 