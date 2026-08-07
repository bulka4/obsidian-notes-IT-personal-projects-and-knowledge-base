Tags: [[_Semantic_search]] [[__AI_systems]]
#SemanticSearch #AISystems 

# Introduction
- Query rewriting means rephrasing the user's query into a clearer or more explicit version while preserving its intent.
	- For example changing `How does it work?` into `How does the HNSW indexing algorithm work?`
- Query expansion means adding related terms or concepts to the query to improve recall (find more relevant documents).
	- For example changing `heart attack` into `heart attack myocardial infarction cardiac arrest`
# How to implement this
## Rule based
Simple dictionaries or rules, for example:
- AI = Artificial Intelligence
- DB = database
## LLM-based
An LLM rewrites or expands the query.
## Knowledge-based
Use ontologies or synonym dictionaries.

Example:
```
car
automobile
vehicle
```
## Embedding-based expansion
Instead of adding words directly:
1. Embed the query.
2. Retrieve some relevant documents.
3. Extract important terms from those documents.
4. Expand the query with those terms.
## Knowledge graph / ontology
Maintain a graph of related concepts.

Example:
```
Vector database
    |
    +-- embeddings
    +-- ANN
    +-- HNSW
    +-- semantic search
```

The system automatically follows these links to expand the query.
## Use conversation context
If the user previously asked:
> "Tell me about HNSW."

Then:
```
"How does it work?"
```

can be rewritten to:
```
"How does the HNSW algorithm work?"
```
## Clarify with the user
If the query is too ambiguous, ask a follow-up question. For example, when a query is `Python`, we can ask `Do you mean the programming language or the snake?`
## Domain-specific assumptions
In a specialized application, the system can safely assume context. 

For example, when a company's internal documentation only contains database topics, then "Replication" almost certainly means "database replication".
