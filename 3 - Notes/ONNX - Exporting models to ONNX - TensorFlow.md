Tags: [[_ONNX]] [[__Machine_Learning]]
#ONNX #MachineLearning 

# Introduction
To export a TensorFlow ([[_Tensorflow|link]]) model into the ONNX format ([[_ONNX|link]]), we can use tools such as `tf2onnx`:
```bash
python -m tf2onnx.convert \
    --saved-model ./saved_model \
    --output model.onnx
```
