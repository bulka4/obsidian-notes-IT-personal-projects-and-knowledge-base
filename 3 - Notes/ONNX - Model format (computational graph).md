Tags: [[_ONNX]] [[__Machine_Learning]]
#ONNX #MachineLearning 

# Introduction
An ONNX model is a serialized computational graph. It describes how inputs are transformed into outputs and contains the model's learned parameters.

It is stored as a `.onnx` file.

The main components are:
- **Graph** — the overall computation.
- **Nodes** — operations in the graph, e.g. `MatMul`, `Add`, `Relu`, `Softmax`.
- **Connections** - Connections between ONNX nodes are tensors flowing from the output of one node to the input of another node
- **Inputs** — tensors provided to the model.
- **Outputs** — tensors produced by the model.
- **Initializers** — stored model parameters/weights.
- **Operators** — standardized operations used by the graph.
- **Metadata** — information such as model version and opset version.