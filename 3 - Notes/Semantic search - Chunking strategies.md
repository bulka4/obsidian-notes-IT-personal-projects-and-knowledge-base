Tags: [[_Semantic_search]] [[__AI_systems]]
#SemanticSearch #AISystems 

# Introduction
Strategies for how to generate chunks ([[Semantic search - Chunking|link]]) for a semantic search:
# Fixed-size chunks
The simplest chunking strategy. Each chunk has a fixed length (the same number of tokens).
# Sentence-based chunking
Each chunk is one sentence. The benefit is that chunks contain complete thoughts but some sentences might be too longs.
# Paragraph/section-based chunking
Use document structure:
```
Document
├── Introduction
├── Architecture
│    ├── Component A
│    └── Component B
└── Configuration
```

Each section becomes a chunk.

Often better for:
- documentation,
- manuals,
- technical papers.
# Semantic chunking
Instead of splitting by length:
1. Start with an empty chunk.
2. Add tokens/sentences.
3. Recalculate the embedding.
4. Measure how much the embedding changed.
5. If the change exceeds a threshold, create a chunk boundary (finish the chunk and start a new one).

Or we could also:
- Calculate an embedding for the next tokens/sentences
- Compare their embedding with the current one
- If their embedding is similar to the current one, include those tokens/sentences in the current chunk

The system detects a topic shift and creates a boundary.

More expensive but can produce better chunks.
