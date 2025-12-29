Tags: [[__Machine_Learning]]

We can calculate the following features for value $x_t$ at any timestep in the time series data:
- Lags - The last $n$ values from the past - $x_{t-1}, ..., x_{t-n}$
- Rolling statistics - Average or maximum from the last $n$ timestamps
- Calendar features - Day of week, month, holiday indicator
- Domain-specific features - temperature anomalies, volatility, humidity, promotions etc.
- Target encoding for categorical variables - Replace each category with a numeric statistic derived for the target variable we want to predict, for example an average.

And additionally:

**_1. Trend/seasonality decomposition_**
Time series decomposition means breaking a series $x_t$​ into simpler underlying components:
$$
x_t = T_t + S_t + R_t
$$
where:
- $T_t$​ = **Trend** — long-term direction (upward/downward)
- $S_t$​ = **Seasonality** — repeating short-term pattern
- $R_t$​ = **Residual (remainder)** — noise or irregular component

Each of those components can be added as a feature to our dataset.

**_2. Fourier features_**
A continuous, smooth way to represent seasonality or periodic patterns in a model — especially for ML models that can’t directly handle cyclic behavior (like linear regression, tree models, or even Transformers without positional encoding).

Instead of using raw “month” or “day of year,” which are discrete and wrap around (December → January), we represent them as sine/cosine pairs:
$$
\begin{aligned}
\text{sin\_term}=sin⁡(\frac{2\pi * t}{P}) \\
\text{cos\_term}=cos⁡(\frac{2\pi * t}{P})
\end{aligned}
$$
where $P$ = period (e.g., 12 for months, 365 for days).

#MachineLearning 