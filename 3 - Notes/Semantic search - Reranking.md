Tags: [[_Semantic_search]] [[__AI_systems]]
#SemanticSearch #AISystems 

# Introduction
The initial vector search may return candidates:
```
top 100 chunks
```

Then a second model can reorder them:
```
Vector search:
fast, approximate

Reranker:
slower, more accurate
```

Example:

Before:
```
1. Chunk A 0.92
2. Chunk B 0.91
3. Chunk C 0.90
```

After reranking:
```
1. Chunk C
2. Chunk A
3. Chunk B
```

because the reranker understands the query-document relationship better.
# Related topics
1. [[Semantic search - Ranking - Cross-encoder reranker]]
2. [[Semantic search - Ranking - Learning-to-rank]]