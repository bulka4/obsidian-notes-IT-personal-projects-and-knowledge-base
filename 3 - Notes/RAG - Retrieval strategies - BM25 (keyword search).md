Tags: [[__AI_systems]] [[__Machine_Learning]] [[__Machine_Learning_Engineering]]
#AISystems #MachineLearning #MLEngineering 

# Introduction
BM25 is a classic lexical search method used in search engines like Elasticsearch:
- It takes a sentence as an input
- Assigns importance scores to words
- Finds related sentences with the same words but sentences containing words with a higher importance score are ranked higher.

Assigning importance score works similar to TF-IDF ([[TF-IDF|link]]). It is done based on how frequently words appear in a single document and in the entire collection of documents:
- If a word appears frequently, it is not important
- If a word appears rarely, it is important.

It is better than TF-IDF in detecting important words. It is done by:
- handling word frequency better
- normalizing document length
- weighting rare words more

Strengths:
- very fast
- great for exact keyword matches
- good for technical terms

Weaknesses:
- doesn’t understand meaning
- fails on paraphrases