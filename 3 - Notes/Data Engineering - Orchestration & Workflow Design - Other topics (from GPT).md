Tags: [[__Data_Engineering]]
#DataEngineering 

# 7. State Management (from GPT)
Pipelines are NOT stateless in reality. We often need to track:
- What was processed
- What failed
- What’s missing

Examples:
- Watermarks in streaming
- Last processed timestamp
- Incremental loads

Problem:
Bad state handling →
- Missing data
- Duplicate processing
# 8. DAG Design Patterns (from GPT)
Common patterns:
- Fan-out / Fan-in
	- Split processing → recombine
- Dynamic pipelines
	- Generate tasks per partition/table
- Modular DAGs
	- Reusable components

Bad DAG:
- One giant script
- Hardcoded logic
- No reuse

 Good DAG:
- Parameterized
- Modular
- Testable
# Questions
- 