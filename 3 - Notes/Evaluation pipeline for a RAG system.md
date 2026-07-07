Tags: [[__AI_systems]] [[__Machine_Learning]] [[__Machine_Learning_Engineering]]
#AISystems #MachineLearning #MLEngineering 

# Introduction
To evaluate a RAG system ([[RAG system|link]]), we create a pipeline like this:
```
Questions dataset
        │
        v
Run RAG system
        │
        v
Collect metrics
        │
        v
Store results
        │
        v
Dashboard
```
where the questions dataset is a dataset with fixed questions, either created manually or created by collecting historical questions from users.

We calculate measures such as:
- Retrieval precision - Of the documents retrieved, how many were actually relevant?
- Retrieval recall - Did we retrieve all the important documents?
- Latency - How long does each step take - embedding generation, vector search, reranking, LLM generation
- Hallucination rate - How often does the model invent information not supported by the retrieved documents?

To measure whether retrieved documents are relevant or whether a model hallucinated, we can use a few a few approaches:
- Human evaluation - A human checks results
- LLM evaluation - Another LLM checks results
- Ground-truth dataset - We create a dataset which contains a question, an expected answer and relevant documents
# Using embeddings for comparing an expected and generated answer
When using a ground-truth dataset, we can compare the generated answer to the expected answer by converting them into embeddings and comparing how similar they are.

But it is less accurate. Two sentences might have similar embeddings (a similar meaning) but still the generated sentence might not be correct, for example:
- Expected answer - "Spark was released in 2014."
- Generated answer - "Spark is a distributed computing framework created by Apache."
In this example, embeddings might be similar but the generated answer is missing the key fact - the year.

This method is good for:
- Filtering obvious bad outputs
- Clustering / analytics - group similar answers or questions
# Online evaluation
We do the same evaluation while users are using the system. We can collect user feedback if available.
# Questions
- 