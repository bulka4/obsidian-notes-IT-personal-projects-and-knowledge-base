This is a collection of documents related to datasets, variables and inputs for machine learning models.

# Introduction
1. [[Dataset used for creating ML models (data points, samples, variables)]]
2. [[Features and target variables]]
3. [[Types of variables used for creating ML models]]
4. [[Sequential data]]
# Converting categorical variables into numeric
1. [[Converting categorical variables into numeric ones]]
2. Types of numeric inputs:
	1. [[Types of numeric inputs for ML models]]
		1. [[Machine Learning models - 1-D input]]
			1. [[Sparse vs Dense vectors]]
		2. [[Machine Learning models - 2-D input]]
		3. [[Machine Learning models - 3-D input]]
3. Methods of converting categorical variables into numeric ones:
	1. [[Encoding categorical variables]]
	2. [[Feature embeddings]]
	3. [[Positional encoding]]
## Converting text into numeric variables
1. [[Converting text into a numeric input for ML models - Overview]]
	- [[Count Vectorization]]
	- [[TF-IDF]]
	- [[Word2vec (word embeddings)]]
# Feature space
1. [[Feature space]]
2. [[Feature space visualization]]
	1. [[Sparsely and densely distributed feature vectors - Visualization]]
	2. [[Multiple feature vector groups - Visualization]]
# Dataset of observations of random variables
1. [[Dataset of observations of random variables X, Y]]
	1. [[Dataset of observations of random variables X, Y - Variables per sample, feature and target variable]]
	2. [[Dataset of observations of random variables X, Y - Variables per feature and target variable]]
2. [[Dataset of observations of random variable X]]
	1. [[Dataset of observations of random variable X - Variables per sample and variable]]
	2. [[Dataset of observations of random variable X - Variables per variable]]
3. [[Dataset of observations of random variables - Explanation]]
# Assumptions about random variables
1. [[Independent and identically distributed (i.i.d.) random variables]]
	1. [[Independent and identically distributed (i.i.d.) pairs of random variables]]
# Mix of continuous and discrete variables
[[Mix of continuous and discrete variables]]
# Time series
- [[Time series as an input for ML models - Overview]]
- [[ML models for different types of time series datasets]]
- [[Time series data - Feature engineering]]
- [[Time series data - Stationarity and transformations]]
# Imbalanced dataset
Before we train a model, we can modify the available dataset which will be used for training, so the model performs better.
1. [[Training ML models on an imbalanced dataset]]
	1. [[Training classification models on an imbalanced dataset]]
		1. Oversampling
			1. [[Random Oversampling]]
			2. [[SMOTE (Synthetic Minority Oversampling Technique)]]
			3. [[ADASYN (Adaptive Synthetic Sampling)]]
		2. Undersampling
			1. [[Random Undersampling]]
			2. [[Tomek links]]
			3. [[Undersampling with cluster centroids]]
		3. Algorithm modification
			1. [[Class Weights - Cost-Sensitive Learning]]
			2. [[Focal loss]]
		4. Balanced Ensemble Methods
			1. [[EasyEnsemble]]
			2. [[Balanced Random Forest]]
	2. [[Training regression models on an imbalanced dataset]]
# Missing data
1. [[Training ML models on a dataset with missing data]]
# Dimensionality reduction
1. [[Dimensionality reduction]]
	1. Feature extraction
		1. [[PCA (Principal Component Analysis)]]
		2. [[Autoencoders - Dimensionality reduction]]
	2. Feature selection
		1. [[Feature selection with a variance threshold]]
		2. [[Pearson Correlation - Dimensionality reduction]]
		3. [[Mutual information - Dimensionality reduction]]
		4. [[Decision Tree - Dimensionality reduction]]
# Feature scaling
1. [[Feature scaling]]
	1. [[Min-Max scaling (Normalization)]]
	2. [[Standarization]]
# Other concepts and techniques
1. [[Training datasets for ML models - Outliers]]