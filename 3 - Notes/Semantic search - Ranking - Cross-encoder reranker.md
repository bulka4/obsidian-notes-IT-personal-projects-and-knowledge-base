Tags: [[_Semantic_search]] [[__AI_systems]]
#SemanticSearch #AISystems 

# Introduction
We can use a cross-encoder ([[Machine Learning - Similarity search - Bi- vs cross-encoders|link]]) for reranking ([[Semantic search - Reranking|link]]) in the following way:
- Use a bi-encoder to retrieve top k the most relevant documents
- Use a cross-encoder to find the most relevant documents out of those k documents

It is better to use cross-encoder only as a reranker, not for reviewing all the documents because it is slow.