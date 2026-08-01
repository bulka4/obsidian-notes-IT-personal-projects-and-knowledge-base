Tags: [[_Databases]] [[_Vector_databases]]
#Databases #VectorDatabases 

# Introduction
Semantic search is about finding text with a similar meaning to the given, another text.

Semantic search is performed this way:
- Take a question
- Convert the question into a vector embedding. That vector represents the meaning of the question.
- Compare our question’s vector to other vectors (created from other sentences) and find the most similar ones. If vectors are similar, that means that sentences represented by those vectors are similar.