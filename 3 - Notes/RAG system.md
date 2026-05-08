Tags: [[__AI_systems]] [[__Machine_Learning]] [[__Machine_Learning_Engineering]]
#AISystems #MachineLearning #MLEngineering 

# Introduction
A RAG (retrieval augmented generation) system is a system, where a LLM generates a sequence using information retrieved from some source which is relevant to the input.

For example, a LLM can answer questions based on a relevant information from a documentation.
# Semantic search and vector database
If we want to create a RAG system for answering questions, in order to find information in a documentation relevant to a question, we need to:
- Create a vector database ([[_Vector_databases|link]]) where we store embeddings ([[Sentence embeddings|link]]) of sentences from the documentation
- Perform semantic search ([[Semantic search|link]]) - use the stored sentence embeddings to find sentences from the documentation relevant to the question
- Generate an answer using the retrieved sentences from the documentation relevant to the question