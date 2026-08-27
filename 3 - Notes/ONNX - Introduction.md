Tags: [[_ONNX]] [[__Machine_Learning]]
#ONNX #MachineLearning 

# Introduction
ONNX (Open Neural Network Exchange) is an open format for representing machine-learning models as computational graphs.

It allows a model created with one ML framework to be exported into a framework-independent format and then executed using different inference engines.

So:
- Different frameworks (e.g. PyTorch, TensorFlow, Hugging Face) can save a model in the ONNX format
- The ONNX Runtime (or different inference engines) can read that model and run it

An ONNX model contains:
- **Graph** — computation represented as nodes and connections
- **Nodes** — operations such as matrix multiplication, activation, normalization
- **Inputs/outputs** — tensors passed into and out of the model
- **Initializers** — model parameters/weights
- **Operators** — standardized operations used by the graph