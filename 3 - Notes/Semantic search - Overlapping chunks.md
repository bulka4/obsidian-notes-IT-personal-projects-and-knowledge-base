Tags: [[_Semantic_search]] [[__AI_systems]]
#SemanticSearch #AISystems 

# Introduction
Overlapping chunks is a chunking technique ([[Semantic search - Chunking|link]]) where consequent chunks have some overlapping tokens, for example for a sentence:
> word1 word2 word3 word4 word5

we might have chunks:
- word1 word2 word3
- word3 word4 word5

This is used to increase a probability that each chunk makes sense, it is not just half of a sentence.

For example:
```
Chunk 1:
"The database uses replication. The primary node is responsible"

Chunk 2:
"The primary node is responsible for accepting writes and synchronizing..."
```
