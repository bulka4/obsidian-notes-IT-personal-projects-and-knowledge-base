Tags: [[_ONNX]] [[__Machine_Learning]]
#ONNX #MachineLearning 

# Introduction
To export a model into the ONNX format ([[_ONNX|link]]) using PyTorch ([[_PyTorch|link]]), we can use the following code:
```python
torch.onnx.export(
    model,
    example_input,
    "model.onnx"
)
```