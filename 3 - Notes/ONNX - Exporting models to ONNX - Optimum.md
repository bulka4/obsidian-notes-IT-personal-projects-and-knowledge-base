Tags: [[_ONNX]] [[__Machine_Learning]]
#ONNX #MachineLearning 

# Introduction
To export a model into the ONNX format ([[_ONNX|link]]) we can use the `optimum-cli` CLI tool:
```bash
optimum-cli export onnx \
    --model bert-base-uncased \
    ./onnx-model
```

It works well for Hugging Face models.