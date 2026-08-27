Tags: [[_ONNX]] [[__Machine_Learning]]
#ONNX #MachineLearning 

# Introduction
An ONNX model is executed by an inference engine/runtime.

Common low-level inference runtimes, offering a lot of flexibility but more complex to use, include:

| Library / engine | Main use                                               |
| ---------------- | ------------------------------------------------------ |
| **ONNX Runtime** | General-purpose ONNX inference; CPU, NVIDIA GPU, etc.  |
| **TensorRT**     | High-performance inference on NVIDIA GPUs              |
| **OpenVINO**     | Optimized inference on Intel hardware                  |
| **Apache TVM**   | Compile/optimize models for different hardware         |
| **OpenCV DNN**   | Lightweight inference, especially computer vision      |
| **DeepSparse**   | Optimized inference for certain sparse neural networks |

And high-level inference runtimes, easier to use but with more limited flexibility, include:
- Optimum - For Hugging Face models
# Related topics
1. [[ONNX - Running ONNX models - ONNX Runtime]]
	1. [[ONNX - Running ONNX models - The onnxruntime Python library]]
		1. [[ONNX - The onnxruntime.InferenceSession Python class]]
	2. [[ONNX - Running ONNX models - The optimum.onnxruntime Python library]]