Tags: [[_My_projects]] [[__Machine_Learning]]
#MyProjects #MachineLearning 

# Introduction
In this project we train a custom Transformer model ([[Transformer model|link]]) for language translation. 
# Programming a Transformer
We program a custom Transformer model in the `Transformer.py` file where we define on our own:
- Multi-head attention layer ([[Neural Network - Multi-Head Attention (MHA) layer|link]])
- Encoder
- Decoder

Model is defined as a class which inherits from the Tensorflow model class ([[Tensorflow - Creating a custom model as a subclass|link]]).

Different parts of this model are programmed:
- Using higher-level abstractions, for example functions for:
	- Dense layer
	- Softmax
	- Embedding layer
- Using functions for basic mathematical operations (e.g. multiplying matrices, reshaping variables) which are used for example in the attention layer for:
	- Splitting and merging heads
	- Calculating dot-product attention
	- Masking

We also program a custom training function for our Transformer model in the `train_transformer.py` file where we:
- Manually calculate loss
- Calculate gradients (using `tf.GradientTape`) 
- Updating model's parameters using those gradients and chosen optimizer (using `optimizer.apply_gradients`)
# Data
Dataset used for training is a CSV file with sentences translated in English and French.