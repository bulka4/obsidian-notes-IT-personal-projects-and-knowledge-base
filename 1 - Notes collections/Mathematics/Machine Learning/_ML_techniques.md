Tags: [[__Machine_Learning]]
#MachineLearning 

# Converting variables from one type to another
## Converting categorical variables into numeric
1. [[Converting categorical variables into numeric ones]]
	1. [[Encoding categorical variables]]
		1. [[Encoding categorical variables - One hot encoding]]
		2. [[Encoding categorical variables - Target - mean encoding]]
		3. [[Encoding categorical variables - Frequency encoding]]
	2. [[Feature embeddings]]
	3. [[Positional encoding]]
### Converting text into numeric variables (NLP)
1. [[Converting text into a numeric input for ML models - Overview]]
	- [[Count Vectorization]]
	- [[TF-IDF]]
	- [[Word2vec (word embeddings)]]
	- [[Sentence embeddings]]
## Converting a continuous variable into discrete
1. [[Feature engineering - Converting continuous features into discrete]]
# Time series data
- [[Time series as an input for ML models - Overview]]
	- [[ML models for different types of time series datasets]]
	- [[Time series data - Feature engineering]]
	- [[Time series data - Stationarity and transformations]]
	- [[Time series data - Train test split (to confirm)]]
# Mix of different types of input variables
[[Machine Learning - Mix of different types of input variables]]
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
			1. [[ML training algorithms for an imbalanced dataset]]
				1. [[Class Weights - Cost-Sensitive Learning]]
				2. [[Focal loss]]
		4. Balanced Ensemble Methods
			1. [[EasyEnsemble]]
			2. [[Cluster-based ensemble]]
			3. [[Balanced Random Forest]]
	2. [[Training regression models on an imbalanced dataset]]
# Missing data
1. [[Training ML models on a dataset with missing data]]
# Dimensionality reduction
1. [[Dimensionality reduction]]
## Feature extraction
1. [[PCA (Principal Component Analysis)]]
2. [[Autoencoders - Dimensionality reduction]]
## Feature selection
1. [[Feature selection with a variance threshold]]
2. [[Pearson Correlation - Dimensionality reduction]]
3. [[Mutual information - Dimensionality reduction]]
4. [[Decision Tree - Dimensionality reduction]]
# Feature engineering
1. [[Time series data - Feature engineering]]
2. [[Feature engineering - Converting continuous features into discrete]]
3. [[Feature engineering - Dropping uncorrelated features]]
## Feature scaling
1. [[Feature scaling]]
	1. [[Min-Max scaling]]
	2. [[Standarization]]
## Representation learning
1. [[Machine Learning - Representation learning]]
	1. [[Feature embeddings]]
	2. [[Word2vec (word embeddings)]]
	3. [[Sentence embeddings]]
# Outliers
1. [[Training datasets for ML models - Outliers]]
