Tags: [[__Machine_Learning]]

# Introduction
As described here - [[Types of numeric inputs for ML models|link]], an input for a model is usually a tensor with up to 4 dimensions. They contain numeric values which can be seen as vectors, for example:
- A 3-D tensor can be seen as a matrix which elements are vectors
- Each row in a 2-D tensor (matrix) is a vector

As described here - [[Types of variables used for creating ML models|link]], numbers which those vectors consist of, are variables of different types representing different features.

In context of machine learning, we usually distinguish two types of input vectors: sparse and dense.
# Sparse vector
A vector in which most entries are zero.

The non-zero values can be binary (0/1) or any numeric values which represents features.
# Dense vector
A vector in which most entries are non-zero, often containing continuous values.

In ML, dense vectors are frequently learned embeddings that capture a meaning of features and relations between them.
# Sparse vectors - Examples
## Words in a sentence
A sparse vector can represent how many times each word (out of all the possible words) appears in a sentence, so each number of that vector corresponds to a specific word. This method is called Count Vectorization ([[Count Vectorization|link]]).

Most of the values will be zero, because most of the words (out of all the possible words), don't appear in one sentence.
## Items ratings (recommendation system)
Numbers in a sparse vector can represent ratings granted to different items, for example movies, by users. Most of the values will be zero, because most people didn't see most of the movies.

Such a data representation in used in recommendation systems using collaborative filtering as described here - [[Recommendation systems - Collaborative filtering]].
# Dense vectors - Examples
## House features
Each number in a dense vector can represent a feature of a house, for example:
- Area
- Number of bedrooms
- Does it have a garden
## Word embeddings
Each word can be converted into a vector, called embedding, representing its meaning and relation to other words. Those vectors are created automatically by a model.

For example, words can be converted into such vectors, that after replacing words with their vector representations the following equation might be true:
$$
\text{'king' - 'men' + 'women'} \approx \text{'queen'}
$$
Or words such as 'shoe' and 'boots' will have similar vectors.

This method is described here - [[Word2vec (word embeddings)|link]].
## Feature embeddings
Categorical features, other than words, can be also converted into embeddings, that is dense vectors representing their meaning and relation to other features. For example, categories like 'cat' and 'dog' will have more similar vectors than 'cat' and 'house', since they are both animals.

It is described here - [[Feature embeddings|link]].

#MachineLearning 