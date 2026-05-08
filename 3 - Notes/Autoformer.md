Tags: [[__Machine_Learning]]
#MachineLearning 

# Introduction
Autoformer is a variant of the Transformer architecture, designed specifically for **time series forecasting** rather than text or general sequence tasks.
# Programming and explaining an Autoformer
This document provides information about where to find code for programming an Autoformer - [[Programming an Autoformer]].

There is also additional explanation of how the Autoformer works using the provided code.
# Useful materials
Useful materials explaining an Autoformer:
- [huggingface.co](https://huggingface.co/blog/autoformer) 
- [arxiv.org](https://arxiv.org/pdf/2106.13008.pdf) 
# Model inputs
Inputs for an Autoformer are:
- time features - for example year, month, day of month. They have shape (no_samples, seq_length, no_time_features) (or maybe (seq_length, no_time_features))
- values - for example number of sold products. They have shape (no_samples, seq_length, values_dim) (or maybe (seq_length, values_dim))
- static features for those values - for example what product has been sold, by which store. Those features are static that means that they are the same for all values. They have shape (no_samples, values_dim) (or maybe (values_dim))

Time features which are an input for a model are being embedded.