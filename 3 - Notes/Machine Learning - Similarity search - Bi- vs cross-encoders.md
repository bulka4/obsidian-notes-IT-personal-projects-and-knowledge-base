Tags: [[__Machine_Learning]] 
#MachineLearning  

# Introduction
When performing a similarity search ([[Machine Learning - Similarity search|link]]), we can use either bi- or cross-encoders:
- bi-encoder is a model which generates an output vector for a query and another object independently, and we compare output vectors to check how similar is this object to the query
- cross-encoder is a model which takes as an input both the query and another object together and generates for them a single output which is a relevance / similarity score.

Bi-encoders are faster because we can generate vectors for all the objects once and store them. Then, when a new query appears, we calculate an output vector only for this query and compare it with already calculated vectors for other objects.

Cross-encoders are slower as they need to always calculate output vectors not just for the query but for all the pairs `(query, object)` for all the objects but it is more precise.