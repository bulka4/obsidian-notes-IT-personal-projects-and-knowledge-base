Tags: [[__Machine_Learning]]

# Introduction
Word2Vec is a feature embedding technique ([[Feature embeddings|link]]) used to convert categorical variables ([[Types of variables used for creating ML models|link]]) with textual values into a numeric variables ([[Converting text into a numeric input for ML models - Overview|link]]).

It uses neural network ([[Neural Network|link]]) that learns to represent words as dense vectors ([[Sparse vs Dense vectors|link]]) (embeddings) in a continuous vector space, where:
- Words with similar meanings are close together
- Relationships between words are captured geometrically (e.g., _king - man + woman ≈ queen_)

So each data sample ([[Features and target variables|link]]) (a document), which is an input for a model, becomes a 2-D tensor (a matrix) ([[Machine Learning models - 2-D input|link]]) of shape $(n, k)$, where:
- Each row correspond to a single word ($n$ words in total per document)
- Each word is represented using $k$ numbers (columns)

Each document needs to have the same shape, so when one document has less words than the other (less than $n$), it has zeros in the remaining rows.

It is trained using one of two methods:
- CBOW (Continuous Bag of Words)
	- Predict a word based on the context, i.e. other words which appear before and after this word
	- For example, given the context 'the cat _ on the mat' predict the missing word 'sat'
- Skip-gram
	- Predict the context words based on the current word
	- For example given 'cat', predict nearby words like 'the', 'sat', 'on'

Words which appear in a similar context, gets assigned similar vectors.

#MachineLearning 