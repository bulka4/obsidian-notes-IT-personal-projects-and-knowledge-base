Tags: [[__MLOps]]
#MLOps 

# Introduction
An online store is useful in a real-time inference, when we need to make prediction irregularly and quickly. When we might need to make a prediction at any point in time.

An online store is an in-memory database (e.g. Redis) where we store features used as an input for a model. Because it is in-memory, reading data from it is very quick and we can use a feature store to read them easily.

Below sections explain how a feature store helps with reading features from an online store.
# Using an online store for a real-time inference
When we calculate new feature values, we save them:
- In an online store first (where we keep only the latest data for inference)
- And then in a data warehouse (where we keep all the historical data for training)

Thanks to this:
- We can make predictions quickly
- Data is consistent during training and inference

Both benefits are explained more in the sections below 'Quick predictions' and 'Feature consistency'.
## Quick predictions
Thanks to reading feature values from an online store, we don't need to wait for computing a feature when making a prediction or reading it from a data warehouse - both are more time consuming than reading from an in-memory database.
## Feature consistency
If we calculate features on the fly in the Python script which makes predictions, we can have the feature calculated in a different way than it was done by the process saving those features in a data warehouse, since Python functions used in that script can work differently.

If we use the same process to save features in an online store and a data warehouse, and use only them for making predictions instead of computing features on the fly in the script that makes predictions, we make sure that we always use a feature calculated in exactly the same way.
# Using a feature store for reading features from an online store
A feature store can make it easier to read features from an online store. We only provide feature's name and a feature store knows:
- where data lives
- how to fetch it
- how to join it

We don't need to provide for example Redis keys, table and column names.

Without a feature store, when we want to read features from an online store, we might need to:
- Read data from multiple sources
- Change a lot of code when source of a feature changes
- Manage joins (join feature tables to an event table)
- Manage schema
## Read data from multiple sources
When we need to get multiple features, we might need to read them from multiple different sources and then our function becomes complex:
```python
def get_features(user_id):
	return {
		"avg_spend": redis.get(...),
		"credit_score": postgres.query(...),
		"last_login": api_call(...)
	}
```
## Changed data source
When a data source where we keep a feature changes, with a feature store we don't need to change the code for reading that feature using a feature store. We only change the definition of that feature in the feature store in a single place.
## Manage joins
A feature store can manage joins between feature tables and an event table. When we define features, we also define what is a key to join it with other tables.

This is especially useful when joining time dependent features like explained here - [[MLOps - Feature store - Time correctness]].
## Manage schema
When data type or field name changes, it might be difficult to figure out why our code doesn't work.

With a feature store, we define what are the data types and field names and when they change and don't match what we defined any more, we get a clear error about it.
# Questions
- 