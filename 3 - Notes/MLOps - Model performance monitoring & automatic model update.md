Tags: [[__MLOps]]
#MLOps 

# Introduction
To monitor performance of ML models, we observe its performance so far and things which can affect future performance:
- Prediction behavior
- Data drift
# Metrics to monitor
## Model performance
Model performance metrics:
- Accuracy, RMSE etc.
## Prediction behavior
Check:
- Prediction mean
- Prediction variance
- Class balance
- Confidence distribution
- feature importance drift monitoring
- SHAP value drift

If those values changes significantly, something might be wrong.

We can calculate some of those values using dbt, and more complicated ones using Python. Results will be saved in a separate table from where can be used for monitoring.
## Data drift
Check for new data:
- Feature distributions
- Null rates
- Cardinality
- Summary stats
- KL divergence
- Wasserstein distance

and compare it with the data used for training. If those values are different, then model can start making worse predictions.

This way we can detect problems with predictions before they appear.
# Tools for monitoring and alerts
We can:
- Use BI tools to observe historical data about metrics listed earlier
- Use tools like Prometheus and Grafana to get alerts when:
	- Performance drops or drift is detected (no retraining is triggered yet but it is worth to look into it)
	- Model gets updated
# Model update
Once we observe that model performance drops, we can automatically train new models and replace an old model with a new one in production pipelines.
# Questions
- 