Tags: [[_My_projects]] [[__Machine_Learning]]
#MyProjects #MachineLearning 

# Introduction
We fine tune here a Hugging Face model so it learns how to create sentence embeddings ([[Sentence embeddings|link]]) which can be used for a semantic search.

We perform fine tuning using the `sentence_transformers` library and the triplet learning method ([[Triplet learning|link]]) where we use 3 inputs for a model:
- Anchor - A reference input
- Positive - An input for which model's output should be similar to the output for the Anchor
- Negative - An input for which model's output should be different than the output for the Anchor

and we train the model in such a way to make the difference between outputs for the Anchor and Positive smaller by at least a specific margin than the difference between outputs for the Anchor and Negative.
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
# Creating sentence embeddings
Using the fine-tuned model from Hugging Face, we create sentence embeddings for:
- Documents from Confluence
- Sentences from an Excel file

We read data from Confluence using Rest API (code is not in this project's repo).