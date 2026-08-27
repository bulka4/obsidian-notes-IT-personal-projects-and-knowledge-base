Tags: [[_ONNX]] [[__Machine_Learning]]
#ONNX #MachineLearning 

# Check name, type and shape
We can check a description of an input and an output, like its name, type or shape like this:
```python
for input in session.get_inputs():
    print(input.name)
    print(input.shape)

for output in session.get_outputs():
    print(output.name)
    print(output.shape)
```

After running this code, we might see for example:
```
Input:
  input_ids       [batch, sequence_length]
  attention_mask  [batch, sequence_length]

Output:
  sentence_embedding [batch, 384]
```
# Use model's documentation
We can check the documentation of the model we use to learn more about what output it produces and what inputs it expects.
# Inspect the computational graph
Examine nodes leading to each output to learn about how this output is created, for example we might see a graph like this:
  ```
	input_ids
	    ↓
	Transformer layers
	    ↓
	token_embeddings ──────────────┐
	                               ↓
	                            pooling
	                               ↓
	                       sentence_embedding
  ```
  
A tool like Netron is particularly useful here: open the `.onnx` file and visually inspect the graph.
# Example model outputs
Examples of what outputs different models can generate:
## Logits
A model can output logits of a shape of:
```
logits.shape = [batch_size, input_sequence_length, vocabulary_size]
```

So model outputs one logit vector `logits[i, j]` per input token which is a prediction for the next token at the position number `(j+1)`.

Each logit vector `logits[i, j]` is of a length of `vocabulary_size` which contains scores for every possible token, the higher score means that this token is more likely to be the token at the position number `(j+1)`.

This is used for token generation. The last logit vector `logits[:, -1, :]` is used to predict the next token in the response.
## Sentence embedding
A model can output a sentence embedding ([[Sentence embeddings|link]]) with a shape of:
```
sentence_embedding.shape = [batch_size, embedding_dimension]
```

The model outputs one embedding vector per input text. Each embedding is a vector of a fixed length, e.g. `384` for `all-MiniLM-L6-v2`.

The values in the embedding vector represent the semantic characteristics of the entire input text. Texts with similar meanings should have similar embeddings.