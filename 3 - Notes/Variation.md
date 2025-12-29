Tags: [[__Machine_Learning]], [[_Probability]], [[__Mathematics]]

# General definition
General variation refers to an average difference between vectors and their mean in a given set of vectors. It is given by the formula:
$$
\large
Variation(C) = \frac{1} {|C|} \sum_{x_i \in C} ||{x_i} - \mu||^2,\ x_i \in \mathbb{R}^d
$$
Where:
- $C$ - Set of vectors
- $|C|$ - Number of elements in the set of vectors $C$
- $\mu$ - Centroid of the set of vectors $C$ (the mean vector)
- $x_i$ - Samples which belongs to the set of vectors $C$ 
# Variation in probability theory
In probability, variation is a specific case of the general variation formula. It is given by this formula:
$$
Var(X) = \frac{1}{n} \sum_{i=1}^n (x_i - \bar{x})^2
$$
Where:
- $\bar{x}$ is a mean of all the vectors $x_1, x_2, ..., x_n$

#MachineLearning  #Probability #Mathematics 