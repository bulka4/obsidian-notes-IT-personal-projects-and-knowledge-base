Tags: [[__AI_systems]] [[__Machine_Learning]] [[__Machine_Learning_Engineering]]
#AISystems #MachineLearning #MLEngineering 

# Introduction 
Instead of dense embeddings, they produce sparse weights over words.

Examples:
- SPLADE
- DeepImpact

What they do:
- take a sentence
- expand it with related terms
- assign importance scores to words

So:
> “Spark partitions data”

might become:
```
spark: 0.9
partition: 0.8
split: 0.7
distributed: 0.6
```

Then search is still keyword-based, but smarter.