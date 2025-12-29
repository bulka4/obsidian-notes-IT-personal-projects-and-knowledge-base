Tags: [[_DeepSpeed]]

# Introduction
Continuous (dynamic) batching is a type of batching ([[Batching|link]]) used in a model which makes multiple predictions one by one, for example when using a transformer model ([[Transformer model|link]]) to generate tokens ([[Token generation|link]]).

Every time we make a new prediction using a model, we can join additional input to the batch or remove one of the inputs from the batch.

When we finished making predictions for one input (there will be no more predictions), then we can return predictions for this input without waiting for further predictions for other inputs from the batch.

Also, during making predictions in a batch, when a new request comes in (new input to make predictions for), and we have some free slot in a batch, we can include this new input in the current batch.

#DeepSpeed 