Tags: [[_Vector_databases]]
#VectorDatabases

# Introduction
Semantic search is about finding text with a similar meaning to the given, another text.

Semantic search is performed this way:
- Take a question
- Convert the question into a vector embedding. That vector represents the meaning of the question.
- Compare our question’s vector to other vectors (created from other sentences) and find the most similar ones. If vectors are similar, that means that sentences represented by those vectors are similar.

We can use for semantic search vector dbs ([[_Vector_databases|link]]):
1. **Create a vector db**
- Convert documents into vector embeddings using LLM
- Save embeddings together with corresponding text in a vector db

2. **Find documents in a vector db similar to the given question**
- Convert a question into a vector embedding using LLM
- Find in a vector db docs with vectors similar the question’s vector