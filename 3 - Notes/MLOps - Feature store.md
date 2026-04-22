Tags: [[__MLOps]]
#MLOps 

# Introduction
A feature store is a system that:
1. Stores features (inputs to ML models)
2. Makes them reusable
3. Ensures consistency between training and serving

In short:
> A feature store is a central place where we keep all the features.
# How a feature store works
A feature store allows us to:
- Define where (in which table and column in a data store) to find a specific feature
- Save features in an in-memory database (online store) and read them from it quickly. Saving features in an online store gives us a quick access to them.
- Provides an API to retrieve features
# Feature as a main object instead of table
The main object which we work with is a single feature, not the entire table which is a collection of many columns.

Thanks to that:
- Each feature has a separate documentation, so we can for example search for features (using their documentation) and compare individual features side by side without looking at entire tables.
- Individual features are versioned. We can check a history for a single feature instead of the entire table. Although, if we want to change how a feature is calculated, we still need to change the SQL code in a data warehouse and version that code.
# What a feature store provides
- **Feature documentation and versioning** - Allows to document individual features to help find the one we need and reuse it ([[MLOps - Feature store - Metadata, documentation and versioning|link]])
- **Online store for real-time inference** - Helps with reading features from an in-memory database from where they can be accessed quickly ([[MLOps - Feature store - Online store for real-time inference|link]])
- **Time correctness** - Helps with properly joining tables with events and features which are defined for a specific time such that we take the latest available feature value and avoid data leakage (using data from the future, not known during making a prediction during training)([[MLOps - Feature store - Time correctness|link]])
# Unified access (offline + online)
When reading data from an offline store (a data warehouse) and online store (in-memory database), we use the same abstraction / API provided by a feature store:
```python
get_historical_features()  
get_online_features()
```
Without it:
- training = SQL
- inference = Redis logic
# Popular tools
- Feast (open source, widely used) ([[_Feast|link]])
- Tecton (managed, enterprise)
- Databricks Feature Store
# Questions
- How does a feature store handle feature history and what is a problem with it?
- 