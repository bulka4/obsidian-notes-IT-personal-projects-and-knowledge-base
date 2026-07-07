Tags: [[__AI_systems]] [[__Machine_Learning]] [[__Machine_Learning_Engineering]]
#AISystems #MachineLearning #MLEngineering 

# Introduction
Conversation memory is used in systems to remember information from earlier messages in a chat so it can use it later.
# Types of memory
## Short-term memory (context window)
- Keep recent messages in the prompt passed to the LLM
- Once the conversation gets too long → older messages are dropped

So it's not real storage — just what fits in the input context. Data is stored only in memory (RAM) in this case.
## Long-term memory (stored data)
Store information from previous conversations in an external database (Redis, vector DB, user profile store).

Example:
```
User: I’m building a RAG system → stored in memory DB
```

Later:
```
Retrieve user facts → inject into prompt
```

Before generating and answer, we can retrieve from the stored conversations relevant information using e.g. semantic search like in a RAG system ([[RAG system|link]]).
## Session memory
Temporary memory for a single session:
- login session
- chat session
- workflow state

It can be stored either in a memory or on a disk.
# How it works in RAG systems
In a RAG system ([[RAG system|link]]), memory usually looks like this:
```
User query   
↓
Retrieve:
	- conversation history
	- user profile (optional)
	- relevant documents
↓
Build prompt
↓
LLM generates answer
```
# Common implementation patterns
## Append history
You just keep adding messages:
```
User: ...
Assistant: ...
User: ...
Assistant: ...
```
## Summarized memory” (scalable)
When history gets too long:
- summarize old conversation
- store summary instead of raw text

Example:
> “User is building a RAG system with LangGraph and Kubernetes.”
