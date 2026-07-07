Tags: [[_Backend_Engineering]]
#BackendEngineering 

# Introduction
Strong consistency is a consistency model ([[Backend Engineering - Distributed microservices - Consistency models|link]]) where Related operations are seen in the same order:
- If A causes B, everyone sees A before B
- Unrelated operations may appear in different orders
# Example:
- “post → comment” ordering in social apps