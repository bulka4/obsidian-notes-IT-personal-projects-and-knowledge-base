Tags: [[__Machine_Learning]], [[_Mathematical_analysis]], [[__Mathematics]]
#MachineLearning #MathematicalAnalysis #Mathematics 

# Introduction
Triplet learning is a technique where we take 3 inputs for a model:
- Anchor - A reference input
- Positive - An input for which model's output should be similar to the output for the Anchor
- Negative - An input for which model's output should be different than the output for the Anchor

where model output is a vector.

We need to choose some measure to calculate a difference / similarity between vectors (e.g. cosine similarity), and we train the model in such a way to make the difference between outputs for the Anchor and Positive smaller by at least a specific margin than the difference between outputs for the Anchor and Negative.

We use for that a loss function like:
$$
\large
L = max(0, d(f(a), f(p)) - d(f(a), f(n)) + m)
$$
where:
- $f(a), f(p), f(n)$ - Model's output for the Anchor, Positive and Negative
- $d(f(a), f(p))$ - A difference / distance between model's outputs for the Anchor and the Positive
- $m$ - Chosen threshold (how big difference between $d(f(a), f(p))$ and $d(f(a), f(n))$ we want)
# Example usage - Embeddings
Triplet learning is commonly used in creating text embeddings which are vectors representing a meaning of a text, such that sentences / words with a similar meaning should get similar embeddings.

So:
- For the Anchor we choose any sentence
- For the Positive we choose a sentence with a similar meaning to the Anchor
- For the Negative we choose a sentence with a different meaning than the Anchor

and a model should create:
- An embedding vector for the Positive input sentence similar to the embedding of the Anchor
- And an embedding vector for the Negative input sentence different than the embedding of the Anchor