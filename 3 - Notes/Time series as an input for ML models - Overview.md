Tags: [[__Machine_Learning]]

# Introduction
Time series data is a subset (an example) of a sequential data ([[Sequential data|link]]). It is a sequential data where each element in a sequence is related to time.

Time series data is a sequence of events / object features appearing in different points in time.
# Different types of time series datasets
There are different types of time series datasets we can use as an input for a model and different model architectures for handling them:
- A single sequence
- Multiple samples with sequences
- Multiple samples with sequences of numbers plus static features
- Multiple samples with sequences of numbers plus dynamic features

More information about them can be found in the document [[ML models for different types of time series datasets|here]].
# ML models for working with time series data
Common models for working with time series data include:
- **Classical models:** ARIMA, SARIMA, Exponential Smoothing
- **Machine learning models:** XGBoost, Random Forest (on lag features)
- **Deep learning models:** RNN/LSTM/GRU, 1D CNN, Temporal Convolutional Networks, Transformers
- **Hybrid approaches:** statistical models with NN residuals or ensembles
# Feature engineering
We can create multiple additional features for a time series dataset which helps with making predictions:
- Lags - The last $n$ values from the past - $x_{t-1}, ..., x_{t-n}$
- Rolling statistics - Average or maximum from the last $n$ timestamps
- Calendar features - Day of week, month, holiday indicator
- Domain-specific features - temperature anomalies, volatility, humidity, promotions etc.
- Target encoding for categorical variables
- Trend/seasonality decomposition
- Fourier features

More information about it can be found in the document [[Time series data - Feature engineering|here]].
# Stationarity and transformations
Some of the models require time series data to be stationary. If it's not, then we can make it stationary by performing transformations.

More information about it can be found in the document [[Time series data - Stationarity and transformations|here]].
# Other topics worth exploring
In the future we can explore the following topics and add them to those notes:
- **Multivariate time series** (multiple correlated variables)
- **Anomaly detection**
- **Missing data and resampling**
- **Seasonality and trend decomposition**

#MachineLearning 