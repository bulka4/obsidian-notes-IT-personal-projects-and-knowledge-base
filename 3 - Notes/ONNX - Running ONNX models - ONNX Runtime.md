Tags: [[_ONNX]] [[__Machine_Learning]]
#ONNX #MachineLearning 

# Introduction
ONNX Runtime is an inference engine used to run ONNX models ([[ONNX - Running ONNX models|link]]). 

We can use it for example through Python libraries such as:
- `onnxruntime`
- `optimum.onnxruntime`
# Execution providers
It can execute the model on different hardware through **execution providers**, for example:
- CPU
- CUDA / NVIDIA GPU
- TensorRT
# Tools
Tools for using the ONNX Runtime:
1. [[ONNX - Running ONNX models - The onnxruntime Python library]]
	1. [[ONNX - The onnxruntime.InferenceSession Python class]]
2. [[ONNX - Running ONNX models - The optimum.onnxruntime Python library]]