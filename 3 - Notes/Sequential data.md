Tags: [[__Machine_Learning]]

# Introduction
Sequential data refers to data which is in form of an ordered list of elements. Changing the order of those elements changes the meaning of data.

In context of machine learning, we say that a dataset for training models ([[Features and target variables|link]]) contains sequential data if we have:
$$
\large \begin{align}
& D = \{(x_1, y_1), \dots, (x_n, y_n)\} = \{(x_i, y_i)\}_{i=1}^n \\
& x_i = (s_{i1}, \dots, s_{im}) \\
& s_{ij} = (s_{ij1}, \dots, s_{ijT}) \\
& s_{ijt} = (s_{ijt1}, \dots, s_{ijtd}) \in \mathbb{R}^d \\
\end{align}
$$
where:
- $D$ - Dataset
- $\large x_i$ - The $i$-th data sample which contains $m$ sequences
- $\large s_{ij}$ - The $j$-th sequence in the $i$-th data sample
- $\large s_{ijt}$ - A feature vector at the $t$-th position (or timestep) in the sequence
- $\large s_{ijtk}$ - The $k$-th feature of the $t$-th feature vector in the sequence, that is a variable which can be of different types ([[Types of variables used for creating ML models|link]])
# Time series data
Time series data is a subset (an example) of a sequential data. It is a sequential data where each element in a sequence is related to time.

Time series data is a sequence of events / object features appearing in different points in time.

More information about it can be found here - [[Time series as an input for ML models - Overview]].
# Examples
## Text
Text is an example of a sequential data. Each sentences is a sequence of words and changing their order changes the meaning of that data.
## DNA
DNA is a sequence of nucleotides (chemicals).

#MachineLearning 