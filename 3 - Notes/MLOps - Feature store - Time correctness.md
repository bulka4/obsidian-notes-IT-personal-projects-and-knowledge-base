Tags: [[__MLOps]]
#MLOps 

# Introduction
When we have a feature and target variable (representing events) we want to predict which are time dependent, i.e. both are defined for a specific point in time, a feature store can help us with two problems:
- Task correctness - Find the latest feature value for a given event (and avoid data leakage, i.e. taking a future feature value when making a prediction during training).
- Feature availability timing - Find the latest feature value for a given event which was available in the system when that event happened.
	- So during training we don't use a feature value which was calculated for the time before the event but it was not saved in the system yet before the event

A feature store can automatically create a logic to join an event table (with events / values of the target variable we want to predict) and a feature table (with feature values) to take the latest feature value for a given event.
# Assumptions about when to use it
This section describes assumptions about a situation when a feature store can help us with time correctness and feature availability timing.
## Event table
Target variable values (events) are time dependent. They are saved in a table with columns:
- Entity key - unique identifier (e.g. `user_id`, `product_id`)
- event timestamp - when an event occurs (e.g. `event_time`)
- Label - target variable value we want to predict
## Feature table
Feature values are calculated for different points in time. They are saved in a table with columns:
- Entity key - unique identifier (e.g. `user_id`, `product_id`)
- feature timestamp - when a feature value was calculated (e.g. `feature_time`)
- feature value
## Example
For example:
- A target variable can indicate whether or not a user clicked on an add 
- A feature can indicate how much time during last 7 days a user has spent reviewing a given category of products.
# Joining an event and a feature table
In order to create a table with a feature value and a target variable we want to predict, we need to join a feature and an event table.

Ideally we would join them on `feature_time = event_time` but that is not always possible. Like in the example about clicking an add, we might calculate feature values once per 10 min (`feature_time` is discrete) while we can try to predict an event at any time (`event_time` is continuous). So for example the latest feature value can be for 13:50 while we make a prediction at 13:53 (there is missing feature data for the last 3min).

So in that case we need to join tables on `feature_time <= event_time` and take the latest feature value.

A feature store can automatically create a logic for such joining.
# Late data
When training a model, we need to take into account not only for which time a feature was calculated but also when that value became available in the system.

For example:
- An event (clicking an add) happened at 13:53
- A feature (user activity from the last 7 days) was calculated for 13:50
- Pipeline that calculated the feature for 13:50 was finished at 13:55
- The latest feature which was saved in the system at 13:53, was the previous one calculated for 13:40

So in the training dataset, the latest feature for an event that occurred at 13:53, is for 13:50, but at the time when the event happened that feature was saved not in the system yet.

So when model will be making predictions in production after training on live data, we will have again features being saved late, and when we try to make a prediction at 13:53, the latest available feature for us will be for 13:40, so that is older one than used during training.

So during training and inference we end up using different features, for different times (we use older data during real inference in production, than we used in training) what can cause that model performs worse.
# Time correctness
Time correctness is about finding the latest feature value for a given event (and avoid taking a future feature value when making a prediction during training), i.e. to join a feature and even table using the `feature_time <= event_time` condition.

It doesn't take into account whether or not that latest feature was available in the system when the event happened. The 'Feature availability timing' problem is about that.
# Feature availability timing
Feature availability timing, just like time correctness, is about finding the latest feature value for a given event (and avoid taking a future feature value when making a prediction during training) but additionally we check when the data about the feature was saved in the system.

So we join a feature and even table using two conditions:
- `feature_time <= event_time`
- `feature_created_timestamp <= event_time`

where `feature_created_timestamp` indicates when given feature value was saved in the system.
# Code example
Below is an example code in Feast ([[_Feast|link]]) of how to define a time dependent feature and join it to an event table:

Define feature source (source of data for the feature):
```python
feature_source = FileSource(
    path="features.parquet",
    event_timestamp_column="feature_time",   # For what time feature was calculated
	created_timestamp_column="created_time"  # When the feature was created
)
```

Define a FeatureView:
```python
user_features = FeatureView(  
    name="user_features",  
    entities=["user_id"],   # JOIN KEY  
    schema=[  
        Field(name="last_month_revenue", dtype=Float32),  
    ],  
    source=feature_source 
)
```

Prepare event data with features:
```python
event_df = pd.DataFrame(...)

training_data = store.get_historical_features(
    entity_df=event_df,
    features=["user_features:last_month_revenue"]
).to_df()
```
