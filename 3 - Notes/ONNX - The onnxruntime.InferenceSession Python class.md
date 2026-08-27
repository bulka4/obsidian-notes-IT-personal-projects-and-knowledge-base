Tags: [[_ONNX]] [[__Machine_Learning]]
#ONNX #MachineLearning 

# Introduction
The `InferenceSession` class from the `onnxruntime` Python library ([[ONNX - Running ONNX models - The onnxruntime Python library|link]]) can be used to run ONNX ([[ONNX - Running ONNX models|link]]) models using the ONNX Runtime ([[ONNX - Running ONNX models - ONNX Runtime|link]]).
# Running a model
[[ONNX - The onnxruntime.InferenceSession Python class - Running a model]]
# Inspect and interpret input and output
[[ONNX - The onnxruntime.InferenceSession Python class - Inspecting model's input and output]]
# Execution providers
It can execute the model on different hardware through **execution providers**, for example:
- CPU
- CUDA / NVIDIA GPU
- TensorRT

We can specify them:
```python
session = ort.InferenceSession(
    "model.onnx",
    providers=["CUDAExecutionProvider"]
)
```