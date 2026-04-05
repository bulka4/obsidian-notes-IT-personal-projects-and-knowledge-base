Tags: [[__MLOps]]
#MLOps 

# Introduction
A **feature store** is a system that:
1. **Stores features** (inputs to ML models)
2. **Makes them reusable**
3. Ensures **consistency between training and serving**

In short:
> A feature store is a **central place to define, compute, store, and serve features**
# Why feature stores exist (the real problem)
Without a feature store:
- Data scientists compute features in notebooks
- Engineers reimplement them in production
- Logic diverges → **training-serving skew**
# What a feature store provides
## 1. Centralized feature definitions
- Define features once
- Reuse across models
## 2. Offline store (for training)
- Historical features
- Used to train models
Typically:
- Data warehouse / data lake (e.g., Parquet, Delta)
## 3. Online store (for inference)
- Low-latency access (milliseconds)
- Used during real-time predictions
Typically:
- Key-value store (Redis, Cassandra, etc.)
# Architecture (simple mental model)
```
            +-------------------+
            |   Data Sources     |
            +-------------------+
                     |
                     v
            +-------------------+
            | Feature Pipelines |
            +-------------------+
              |              |
              v              v
     +----------------+   +----------------+
     | Offline Store  |   | Online Store   |
     | (historical)   |   | (low latency)  |
     +----------------+   +----------------+
              |              |
              v              v
        Model Training     Model Serving
```
# Types of features (important distinction)
## 1. Batch features
- Precomputed
- Updated periodically (e.g., daily)

Example:
- `avg_spend_last_30_days`
## 2. Real-time features
- Computed on the fly

Example:
- `current_cart_value`
## 3. Streaming features
- Updated continuously

Example:
- `clicks_last_5_minutes`
# Point-in-time correctness (very important concept)
When training:
> You must use **only data that was available at that time**

Example:
- Predict fraud at time T
- Don’t use transactions from T+1 ❌

Feature stores help enforce:  
>**no data leakage**
# Feature store capabilities
- Feature versioning
	- Track changes to feature definitions
- Backfilling
	- Recompute features for historical data
- Feature discovery
	- Search existing features (avoid duplication)
- Metadata & lineage
	- Who created feature?
	- How is it computed?
- Serving APIs
	- Fetch features for inference:
		```
		{  
		  "user_id": 123,  
		  "features": {  
		    "avg_spend_30d": 250,  
		    "transactions_7d": 5  
		  }  
		}
		```
# Popular tools
- Feast (open source, widely used)
- Tecton (managed, enterprise)
- Databricks Feature Store
