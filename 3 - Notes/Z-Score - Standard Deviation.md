Tags: [[__Machine_Learning]]

# Introduction
Z-Score / Standard Deviation is a method for anomaly detection ([[Anomaly Detection models|link]]). I measure how far are data points from the mean in units of standard deviation.

It allows us to detect anomalies based on a single feature at a time, we can't consider multiple features at once with this method.
# How it works
For a dataset $[x_1, \ldots, x_n]$ which is a collection of features:
$$
x_i \in \mathbb{R}
$$
we calculate the mean:
$$
\mu = \frac{1}{n} \sum_{i=1}^n x_i
$$
and standard deviation:
$$
\sigma = \sqrt{\frac{1}{n} \sum_{i=1}^n (x_i - \mu)^2}
$$
Then, we calculate the Z-Score for each data point $x_i$ :
$$
z_i = \frac{x_i - \mu}{\sigma}
$$

The higher is the absolute value $|z_i|$, the more outstanding from the norm given point $x_i$ is.

So we can choose a threshold $z$, and all the points $x_i$ for which the Z-score is above this threshold:
$$
\{ x_i:\ |z_i| > z \}
$$
are considered anomalies (outliers).
# When to use it
This method works the best when:
- Data is approximately normally distributed
- There are no big outliers initially (they distort mean/std)
- There is a single feature based on which we can detect outliers
# Weaknesses
- Very sensitive to outliers
- Not good for multimodal or skewed data:
	- Multimodal data: a dataset which distribution have multiple peaks or clusters instead of one central hump.
	- Skewed data: a dataset which distribution is not symmetric around the mean — one tail is longer than the other.

#MachineLearning 