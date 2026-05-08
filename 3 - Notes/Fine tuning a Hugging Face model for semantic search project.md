Tags: [[_My_projects]] [[__Machine_Learning]]
#MyProjects #MachineLearning 

# Introduction
We fine tune here a Hugging Face model so it learns how to create sentence embeddings ([[Sentence embeddings|link]]) which can be used for a semantic search.

We create sentence embeddings for:
- Sentences from an Excel file
- Documents in Confluence

We perform fine tuning using the `sentence_transformers` library and the triplet learning method ([[Triplet learning|link]]) where we use 3 inputs for a model:
- Anchor - A reference input
- Positive - An input for which model's output should be similar to the output for the Anchor
- Negative - An input for which model's output should be different than the output for the Anchor

Also, this repository contains code for saving models from Hugging Face in the onnx format and converting them into Tensorflow models.
# Code repository
The repository with code for this project is here - [github.com](https://github.com/bulka4/fine_tune_hf_model_for_semantic_search).
## Functions and libraries used in code
For training, we use:
- The `sentence_transformers.losses.TripletLoss` loss function
- The `fit` method from the `sentence_transformers` library:
  ```python
  import sentence_transformers as st
  # Load the model from Hugging Face
  model = st.SentenceTransformer(model_url)
  
  # Define the loss function for triplet learning
  train_loss = losses.TripletLoss(...)
  
  # Prepare training dataset to be used in the model.fit() method
  train_dataloader = DataLoader(x_train, shuffle=True, batch_size=16)
  
  # Fine tune the model
  model.fit(train_objectives = [(train_dataloader, train_loss)], ...)
  ```
## Measures to calculate distance between model's outputs
In order to measure distance between model's outputs for Anchor, Positive and Negative, we use different measures, such as:
- Dot product similarity
- Cosine similarity
- Euclidean distance
# Converting a Hugging Face model into a Tensorflow one
We create a Tensorflow model using the Hugging Face model and the `TFAutoModel.from_pretrained` function in the `TFSentenceTransformer` class / script.
# Saving a Hugging Face model in the onnx format
Below sections describe how to save a Hugging Face model in the onnx format. More notes about it are also here - [[Saving a Hugging Face model in the onnx format]].
## convert.py script
The `convert.py` script can be used convert models from Hugging Face into the onnx format (I didn't create this file and I don't remember where does it come from). We can do this by running the command:
```
py -m convert --quantize --task default --model_id model_path
```
where `model_path` is a path where we saved the model using the following Python code:
```python
import sentence_transformers as st

model = st.SentenceTransformer('model_name/url')
model.save('model_path')
```
## Optimum CLI
Another option for saving Hugging Face models in the onnx format is to use an optimum CLI:
```bash
# Install the package
pip install optimum[onnxruntime]

# Use the package to save a model in the onnx format
optimum-cli export onnx \  
--model bert-base-uncased \  
onnx_model/
```
# Creating sentence embeddings
Using the fine-tuned model from Hugging Face, we create sentence embeddings for:
- Documents from Confluence
- Sentences from an Excel file

We read data from Confluence using Rest API (code is in another repository - [github.com](https://github.com/bulka4/confluence_api)).