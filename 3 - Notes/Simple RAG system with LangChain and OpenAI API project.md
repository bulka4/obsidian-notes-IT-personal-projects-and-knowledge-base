Tags: [[_My_projects]] [[__Machine_Learning]]
#MyProjects #MachineLearning 

# Introduction
This project is a simple Python script which:
- Loads text from text and pdf files from a folder
- Creates embeddings for those files and stores them in an index (in-memory vector database)
- When user asks a question, it gathers text related to that question (finds similar embeddings)
- A LLM answers a question

LLMs are used using external APIs (OpenAI).

LangChain is used for:
- Creating embeddings
- Creating in-memory vector database (FAISS)

Repository with code: [github.com](https://github.com/bulka4/simple_RAG_LangChain_OpenAI_API).