Tags: [[__Machine_Learning]]

# Stationarity
## Introduction
A stationary time series is one whose statistical properties - mean, variance, and autocorrelation - do not change over time.

Some models require time series data to be stationary to work properly.
## Details
Formally, a time series $x_t$​ is strictly stationary if the joint distribution of $(x_t,x_{t+k},x_{t+m},...)$ is the same for all time shifts.  
In practice, we usually care about weak (or covariance) stationarity, which means:
1. The mean $E[x_t]$ is constant over time.
2. The variance $Var[x_t]$ is constant over time.
3. The autocovariance between $x_t$​ and $x_{t+k}$ depends only on k (the lag), not on time t.

If a series is stationary, its patterns don’t depend on where you look in time.  
So, the same model parameters can describe the whole process - which is why many models (like ARIMA) require stationarity.

If a series is non-stationary, it typically has one or more of:
- a trend (mean increases or decreases over time),
- seasonality (periodic fluctuations),
- changing variance (heteroscedasticity).

## Why is stationarity important?
It is important to check whether or not time series data is stationary because some of the models (e.g. ARIMA, SARIMA, VAR) require it.

Some models (e.g. LSTMs, Transformers) can handle non-stationarity but even there stationarity is helpful.

## How to detect non-stationarity?
- **Visual inspection**
    - Look for trends or seasonal patterns in the plot.
    - Plot rolling mean and variance (should be roughly constant if stationary).
- **Statistical tests**
    - **ADF (Augmented Dickey–Fuller) test:**  
        Null hypothesis = _series is non-stationary_.  
        If p-value < 0.05 → reject null → likely stationary.
    - **KPSS test:**  
        Null hypothesis = _series is stationary_.  
        If p-value < 0.05 → reject null → likely non-stationary.
    - Often used **together** for robustness.
- **Autocorrelation Function (ACF) plot**
    - For stationary data, correlations decay quickly to zero.
    - For non-stationary, they persist (slow decay).
# Transformations
Transformations are performed on time series data in order to achieve stationarity. Different methods of transformations are described below.

## Differencing
Subtract each value from its previous one:
$$
y_t = x_t - x_{t-1}
$$
A few facts about this method:
- Removes trend
- If still non-stationary, you can difference again (“second-order differencing”).
- Common in ARIMA (the “I” = Integrated).

## Seasonal differencing
Remove recurring seasonal patterns:
$$
y_t = x_t - x_{t-s}
$$
where s = season length, e.g. 12 for monthly data with yearly seasonality.

## Log transform
$$
y_t = \log(x_t)
$$
Stabilizes **variance** (especially for exponential growth).  
Useful when data are strictly positive and variance increases with mean.

## Square root / Box–Cox transform
Box–Cox is a general power transform:
$$
yt=\frac{x_t^\lambda - 1}{\lambda}​
$$
- Helps stabilize variance and normalize distributions.
- Automatically chooses optimal λ.
- Use only if all values are positive.

## Detrending / Deseasonalizing
Explicitly model and subtract trend/seasonal components using:
- **Decomposition** (e.g., STL, seasonal_decompose) - Mentioned in the 'Feature engineering techniques' section earlier in this document
- **Polynomial regression** on time
- **Fourier terms** for periodicity

After removing components, the residuals are usually stationary.

## Standardization or scaling
Even if data are stationary, scaling helps:
- For neural networks and distance-based methods.
- Apply scaling (mean–variance or min–max) _after_ differencing/log transform.

#MachineLearning  