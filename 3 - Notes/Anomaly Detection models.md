Tags: [[__Machine_Learning]]

# Introduction
Anomaly detection is a task of detecting very rare cases, when target variable we want to predict has very rare values.

Below are described different methods for this detecting anomalies.
# Statistical methods
These methods assume data follows some statistical distribution.
## Z-Score / Standard Deviation
More information about it is here - [[Z-Score - Standard Deviation|link]]
- Compute how many standard deviations a point is from the mean.
- Good for: simple, univariate, approximately Gaussian data
- Limitation: not good for complex or multimodal distributions.
## Parametric models
- Fit a distribution (e.g., Gaussian, Poisson) and flag low-probability points.
- Examples:
    - Gaussian Mixture Models (GMM) - [[Gaussian Mixture Models (GMM)|link]]
    - ARIMA residual analysis (for time series)
- Good for: well-behaved distributions, time series forecasting
- Limitation: can be sensitive to assumptions.
## Non-Parametric Models
- KDE (Kernel Density Estimation)
- Quantile-based detection
- Good for: flexible distributions with no known parametric form
# Distance- and Density-Based Methods
These methods detect anomalies by comparing each point’s local neighborhood.
## k-Nearest Neighbors (k-NN)
More information: [[K nearest neighbors (KNN)|link]]
- Computes distance of point to its nearest neighbors.
- Good for: tabular data with meaningful distances
- Limitation: expensive for large datasets.
## Local Outlier Factor (LOF)
- Measures local density; anomalies have lower density than neighbors.
- Good for: non-uniform densities
- Widely used baseline.
## DBSCAN
- Clusters based on density; points not belonging to clusters are anomalies.
- Good for: spatial clustering + anomaly detection
# Clustering-Based Methods
Use clusters to represent “normal” behavior.
## K-means
More information: [[K means clustering|link]].
- Points far from cluster centroids are anomalies.
- Good for: simple, high-dimensional data
- Limitation: assumes spherical clusters.
## Isolation Forest
- Randomly splits data; anomalies are isolated with fewer splits.
- Good for:  
    - high dimensional data  
    - nonlinear patterns  
    - large datasets
- Very fast and widely used in industry.
# Machine Learning / Predictive Models
Train a model on normal data (without anomalies) and detect deviations from predictions.
## One-Class SVM
- Learns a boundary around normal data.
- Good for: high-dimensional, nonlinear data
## Autoencoders (Neural Networks)
More information can be found here - [[Autoencoders - Anomaly detection|link]].
- Train to reconstruct normal data; anomalies have high reconstruction error.
- Variants:
    - Denoising Autoencoders
    - Variational Autoencoders (VAE)
    - Convolutional Autoencoders (for images)
    - LSTM Autoencoders (for sequences/time series)
## Forecasting Models
- Train a forecast model and evaluate residuals.
- Examples:
    - ARIMA
    - Prophet
    - LSTM/Transformer models
- Good for: time series anomalies
# Graph-Based Methods (Advanced)
Useful when data has relationships or structure.
## Graph Neural Networks
- Node or edge anomaly detection
- Common in fraud detection, network traffic analysis.
## Random Walk / PageRank-based
- Anomalies have abnormal connectivity.


#MachineLearning 