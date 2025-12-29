Tags: [[__Machine_Learning]]

# Introduction
TF-IDF is a method for encoding categorical variables ([[Encoding categorical variables|link]]) with textual values into numeric variables ([[Converting text into a numeric input for ML models - Overview|link]]). 

It is an extension of the Count Vectorization ([[Count Vectorization|link]]) method. It also creates a matrix of word counts but additionally, number for each word is multiplied by its weight.

So it also creates a dataset of shape $(n, k)$ where:
- Rows correspond to documents ($n$ documents in total
- Columns correspond to words (one column per word, $k$ columns in total)
- Values indicates how many times a given word occurred in a given document.

and each data sample, which is an input for a model, is a 1-D tensor (a vector) of length $k$ ([[Machine Learning models - 1-D input|link]]).

For every word we calculate a weight which indicates how important a given word is in a collection of documents. It is calculated using the following rules:
- If a word appears frequently in one document -> increase a weight (importance)
- If a word appears frequently in every document -> decrease a weight
# How it works
Weights are calculated using the Term Frequency (TF) and Inverse Document Frequency (IDF) values:
$$
TF(t, d) = \frac{\text{number of times term t appears in document d}}{\text{total number of terms in d}}
$$
Where:
- $t$ indicates a term (word)
- $d$ indicates a document
$$
IDF(t)=\log(\frac{N}{1 + n_t}​)
$$
Where:
- $N$ - total number of documents
- $n_t$ - number of documents containing the term (word) $t$

The TF-IDF weight for each word (term) is calculated using the following formula:
$$
TFIDF(t, d) = TF(t, d) * IDF(t)
$$

#MachineLearning  