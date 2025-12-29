Tags: [[__Machine_Learning]]

# Introduction
Count Vectorization is a method for encoding categorical variables ([[Encoding categorical variables|link]]) with textual values into numeric variables ([[Converting text into a numeric input for ML models - Overview|link]]). 

It converts a collection of text documents into a matrix of word counts. It tells us how many times each word occurs in each document.

That creates a dataset of shape $(n, k)$ where:
- Rows correspond to documents ($n$ documents in total
- Columns correspond to words (one column per word, $k$ columns in total)
- Values indicates how many times a given word occurred in a given document.

So each data sample, which is an input for a model, is a 1-D tensor (a vector) of length $k$ ([[Machine Learning models - 1-D input|link]]).

#MachineLearning 