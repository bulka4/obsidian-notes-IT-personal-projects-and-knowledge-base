Tags: [[_Databases]] [[_Vector_databases]]
#Databases #VectorDatabases 

# Introduction
Sometimes, when looking for vectors similar to the query ([[Machine Learning - Similarity search - Nearest neighbor search|link]]), we can use metadata to perform initial filtering and then find similar vectors in that filtered dataset.

For example, if we have chunks with metadata like this:
```
Document chunks:

1. "How to configure AWS networking"
   metadata:
       company="AWS"

2. "How to configure Azure networking"
   metadata:
       company="Microsoft"
```

then both chunks are similar semantically to a query "How do I configure networking?" but we can filter results for `company="AWS"` to narrow down results.
# Pre- and post-filtering
We can use metadata filtering before (pre-filtering) or after (post-filtering) performing a semantic search.