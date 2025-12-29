Tags: [[__Machine_Learning_Engineering]]

# Introduction
This component standardizes how you **package, save, and load ML models** regardless of framework (TensorFlow, PyTorch, Scikit-learn, XGBoost, etc.).

- Models are saved in a standard format, with metadata describing how to load and serve them
- Supports multiple deployment flavors (options for loading and serving a model) like Python function, REST API, Spark UDF, or even batch transforms

Saved models can be stored anywhere. One option is MLflow Registry.

#MLEngineering 