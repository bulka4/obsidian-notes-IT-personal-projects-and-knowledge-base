Tags: [[__Machine_Learning]]
#MachineLearning 

# Introduction
Sentences can be converted into embeddings (similarly like words - [[Word2vec (word embeddings)|link]]), i.e. vectors which represents a meaning of those sentences and which captures relations between sentences, such that for example similar sentences get created similar embeddings (i.e. a difference / distance between those vectors is small).

Converting sentences into embeddings can be used for example for a semantic search ([[Semantic search|link]]).
# Training a model to create sentence embeddings
There are different tasks we can give to a model so it learns how to create effectively creating sentence embeddings:
## Seq2seq
Here's how it works:
- A seq2seq model (sequence to sequence) is a model which takes a sequence as an input and generates another sequence
- A seq2seq model has two components:
	- **Encoder**:
		- Takes the input sequence as an input and generates a vector as an output
		- The output is an embedding for the input sequence
	- **Decoder**:
		- Generates the output vector (a sequence) elements one by one
		- Takes as an input the Encoder's output (an embedding) and elements of the output vector generated so far

So the encoder learns how to create an embedding which contains enough information about the input sequence so the decoder can use it for some task (generating some output sequence).

To train an encoder to create effective sentence embeddings, we can train a seq2seq model for tasks such as:
- Recreating the input sequence - based on an input sequence, predict its elements one by one (like an autoencoder)
- Predicting next and previous sentence based on current sentence
- Predicting an answer for a question
- Translation
## Classification
If we train a model for a classification like that:
```
input -> encoder -> embedding -> classifier -> label
```
where:
- encoder - A model whose output is an embedding for the input sequence
- classifier - Another transformation with trainable parameters (e.g. a dense neural network layer ([[Neural Network - Fully-connected (dense) layer|link]]))

then during learning how to predict a label, the encoder can learn how to create an embedding for the input sequence which contains useful information about that sequence and can create similar embeddings for similar sequences to reduce loss.

We can train such a model for such tasks as:
- Predicting if a premise entail or contradict a hypothesis or if they are neutral (using Snli dataset)
- Predicting if 2 sentences are paraphrases
- Question classification
- Predicting how similar are 2 sentences (similarity score is a discrete value between 1 and 5)
- Question answering: choosing one out of multiple possible answers
## Regression
Similarly like in case of classification, we can train a model for a regression like that:
```
input -> encoder -> embedding -> regression model -> label
```
where:
- encoder - A model whose output is an embedding for the input sequence
- regression model - Another transformation with trainable parameters (e.g. a dense neural network layer ([[Neural Network - Fully-connected (dense) layer|link]]))

We can train it for such tasks as:
- Predicting how similar are 2 sentences (similarity score is a continuous value between 0 and 1)
- Providing query, positive and negative sentences and using triplet objective function
## MLM
some words of a sentence are masked (hidden) and model tries to predict those words.
## Corrupting and reconstructing a document 
Corrupting and trying to reconstruct a document like in pre-training of a BART model.
# Projects
Projects related to creating sentence embeddings:
- [[LSTM seq2seq semantic search project]]
- [[Fine tuning a Hugging Face model for semantic search project]]