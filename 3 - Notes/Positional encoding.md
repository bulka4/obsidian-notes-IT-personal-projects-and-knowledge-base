Tags: [[__Machine_Learning]]

# Introduction
When we work with sequential data ([[Sequential data|link]]), and we convert variables (features) at each position in a sequence into embeddings ([[Feature embeddings|link]]), sometimes our model is not able to recognize an order of vector embeddings (features) in a sequence, for example a transformer model ([[Transformer model|link]]).

In that case, we need to additionally add to those embedding vectors additional vectors, which add information about an order of embedding vectors (features) in a sequence.

That operation of adding vectors with information about a position of embedding vectors in a sequence is called positional encoding.

#MachineLearning 