Tags: [[_ONNX]] [[__Machine_Learning]]
#ONNX #MachineLearning 

# Introduction
The `optimum.onnxruntime` Python library can be used to run ONNX ([[ONNX - Running ONNX models|link]]) models using the ONNX Runtime ([[ONNX - Running ONNX models - ONNX Runtime|link]]).

It is a higher-level tool than the `InferenceSession` ([[ONNX - The onnxruntime.InferenceSession Python class|link]]) class, i.e. it is easier to use but offers less flexibility. 

There are different `ORTModelFor...` classes for different tasks:
- `ORTModelForFeatureExtraction` - for feature extraction/embeddings
- `ORTModelForSequenceClassification` - for classification
- `ORTModelForCausalLM` - for generative causal language models
# Model compatibility with the `ORTModelFor...` class
Some models might not work with the `ORTModelFor...` class from the `optimum.onnxruntime` library because for example this class might expect the model to have a specific output with a specific name which this model doesn't have (e.g. an output called `last_hidden_state`). 

In this case, using `InferenceSession` might work.