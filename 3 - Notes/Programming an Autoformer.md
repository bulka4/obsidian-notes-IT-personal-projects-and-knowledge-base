Tags: [[__Machine_Learning]]
#MachineLearning 

# Introduction
This repository - [github.com](https://github.com/thuml/Autoformer/tree/main) contains code for an Autoformer model ([[Autoformer|link]]). It is programmed using PyTorch and the main modules are in the `layers` and `models` folders.

The most important part of this code is also in my private repository - [github.com](https://github.com/bulka4/transformer_family_models).
# Hugging Face functions for building an Autoformer
Hugging Face functions for building an Autoformer - [huggingface.co](https://huggingface.co/docs/transformers/model_doc/autoformer).
# Model inputs
## Time features
In the repository, time features which are an input for a model and which will be embedded, are probably those arguments from the files `classes/Embed.py` and `classes/Autoformer.py`:
- `x` argument for the `TemporalEmbedding` function
- `x_mark` argument for the `DataEmbedding_wo_pos` function
- `x_mark_enc` and `x_mark_dec` arguments for the `Model.forward()` function

They are vectors of shape (`no_samples`, `seq_length`, `no_time_features`) (or maybe they have shape (`seq_length`, `no_time_features`)) where each time feature is a number:
- `x[i, i, 0]` represents a month
- `x[i, i, 1]` represents a day
- `x[i, i, 2]` represents a weekday
- `x[i, i, 3]` represents a hour
- `x[i, i, 4]`represents a minute

Those time features `x[i, j, 0], x[i, j, 1], x[i, j, 2], x[i, j, 3], x[i, j, 4]` will be converted into vectors using the Embedding layer just like words are being converted into word embeddings.

This time feature vector `x` is also the `past_time_features` argument for the `AutoformerModel.forward()` function from Hugging Face ([huggingface.co](https://huggingface.co/docs/transformers/model_doc/autoformer#transformers.AutoformerModel)).

So for example if:
- `x` is our time series data of shape (`no_samples`, `seq_length`, `measurement_dim`)
- `x_time_features` are our time features of shape (`samples`, `seq_length`, `no_features`)
- `x[i, j, k]` is a measurement made on 11th August at 10:15 

then `x_time_features[i, j] = [8, 11, 10, 15]`.
## Static features
Probably static features for a model will be also embedded like time features.