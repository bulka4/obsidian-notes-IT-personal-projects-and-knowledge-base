Tags: [[__Machine_Learning]]

# Introduction
SVD is a method for creating a recommendation system ([[Recommendation systems|link]]). 

In SVD we try to approximate the rating matrix, marked as $R$, where rows correspond to users, columns corresponds to items and values are rates granted items by users. Some values of this matrix are unknown (some users didn't rate some items yet).

We try to approximate the $R$ matrix by multiplying three smaller matrices:
$$
R \approx U \Sigma V^T
$$

Where:
- $U$ - User matrix. Each row represents a user which is a set of features of that user (each column is some feature).
- $V$ - Item matrix. Each row represents an item which, like in the user matrix, is a set of features.
- $\Sigma$ - Scales how important each factor in user and item matrices is.

$U$ and $V$ matrices are made of trainable parameters. We use known ratings from the $R$ matrix to modify (train) those parameters using gradient descent.

#MachineLearning 