Tags: [[_Hugging_Face]] [[__Machine_Learning_Engineering]]
#HuggingFace #MLEngineering 

# Optimum CLI
In order to save a Hugging Face model in the onnx format, we can use the optimum CLI tool:
```bash
# Install the package
pip install optimum[onnxruntime]

# Use the package to save a model in the onnx format
optimum-cli export onnx \  
--model bert-base-uncased \  
onnx_model/
```
# Convert.py script
We can also use the `convert.py` script from one of the projects as described in project's documentation - [[Fine tuning a Hugging Face model for semantic search project|link]] in the "Saving a Hugging Face model in the onnx format > convert.py script" section.