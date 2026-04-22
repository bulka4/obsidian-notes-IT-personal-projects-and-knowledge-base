Tags: [[__Machine_Learning_Engineering]]

# Introduction
MLflow let's us to save and read models in a standardized way. It provides an API for that and is compatible with many frameworks (TensorFlow, PyTorch, Scikit-learn, XGBoost, etc.):
- Models are saved in a standard format, with metadata describing how to load and serve them
- Supports multiple deployment flavors (options for loading and serving a model) like Python function, REST API, Spark UDF, or even batch transforms

Saved models are stored in an artifact store (object storage) by a tracking server ([[MLflow - Tracking server|link]]) and they can be added to a MLflow Registry ([[MLflow - Registry|link]]).

#MLEngineering 