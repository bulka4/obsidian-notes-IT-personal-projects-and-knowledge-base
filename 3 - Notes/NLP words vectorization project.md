Tags: [[_My_projects]] [[__Machine_Learning]]
#MyProjects #MachineLearning 

# Introduction
In this project we convert words into vectors using:
- TF-IDF method ([[TF-IDF|link]])
- Word2Vec ([[Word2vec (word embeddings)|link]]) (we train our own model to convert words into embeddings)
# Project code repository
A repository with a code for this project is here - [github.com](https://github.com/bulka4/nlp_words_vectorization).
# Data
We use CSV files from the `data` folder with data about:
- Sentences from Simpsons
# TF-IDF
For calculating TF-IDF we use:
- The `TfidfVectorizer` function from `sklearn`.
- Our own custom function (from the `functions/tf_idf.py` script)
# Word2Vec
For training a Word2Vec model we use the `gensim.models.Word2Vec` class and the `Word2Vec.train` method.
# Finding phrases
We use `Phrases` and `Phraser` functions from the `gensim.models.phrases` module to find phrases, i.e. multi-word expressions (bigrams and trigrams, etc.), e.g. "machine learning" or "New York".

