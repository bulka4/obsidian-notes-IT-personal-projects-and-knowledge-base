Tags: [[_Semantic_search]] [[__AI_systems]]
#SemanticSearch #AISystems 

# Introduction
Learning-to-rank (LTR) is a machine learning approach for learning how to order search results.

Instead of manually defining ranking rules:
```
score =
  0.5 * keyword_match +
  0.3 * popularity +
  0.2 * freshness
```

we train a model to learn the ranking function from data.

Input features can include:
- Query and document
- keyword similarity
- vector similarity
- document length
- freshness
- user clicks
- other metadata

Common approaches:
- **Pointwise** → predict relevance score for each document independently
- **Pairwise** → learn which of two documents should rank higher
- **Listwise** → optimize the whole ranking list

Examples of LTR algorithms:
- LambdaMART
- RankNet
- XGBoost ranking models