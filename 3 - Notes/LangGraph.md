Tags: [[__Machine_Learning_Engineering]], [[_LangChain]]
#MLEngineering #LangChain 

# Introduction
Official documentation and tutorial: [langchain-ai.github.io/langgraph](https://langchain-ai.github.io/langgraph/concepts/why-langgraph/).

LangGraph is a tool for AI agents orchestration. For example it enables creating a workflow where:
- We use multiple LLMs
- Allow LLMs to use additional tools
- Add memory from conversations
- Add steps where human can check and approve agent actions
# Multi-agent orchestration
We can use LangGraph for a multi-agent orchestration where multiple tasks performed by multiple agents.

For example, we can create a workflow where we use multiple agents to answer a question based on available documentation. It works in the following way:
- User ask a question
- The ‘Retriever’ agent converts this question into a vector embedding and retrieves from a vector db documents with similar vector embeddings.
- The ‘Answer’ agent uses the retrieved documents to generate a final answer.
# How it works
Here is how it works:
- Each agent takes as an input the state argument, which is a dictionary, and modifies it
- An agent is dependent on another agent, if it is using state’s key created by the other agent
- We can run multiple agents in parallel if they are not dependent on each other
- Each agent only runs once all its dependencies (parent nodes) produced their outputs

For example, we can create a workflow using two agents and LangGraph like shown below.

One ‘Retriever’ agent is performing a semantic search using a vector database. It finds relevant documents, similar to the given question:
![[2 - Images/LangGraph/Screenshot 1.png]]

This agent:
- Takes as input the state dictionary
- Reads a query (question) from it
- Add a new key to the state about retrieved relevant documents

Second ‘Answer’ agent is generating an answer to a question using documents found by the ‘Retriever’ agent before:
![[2 - Images/LangGraph/Screenshot 2.png]]

This agent:
- Takes as input the state dictionary
- Reads from it information about the documents retrieved by the Retriever agent
- Generates an answer
- Modifies the state such that it contains now only the ‘answer’ and ‘retrieved_docs’ keys

Then we specify the workflow for those agents like here:
![[2 - Images/LangGraph/Screenshot 3.png]]

This indicates that:
- The initial input will go to the Retriever agent
- The state dictionary prepared by the Retriever agent (with a new ‘retrieved_docs’ key) will be an input for the Answer agent
- Output from the Answer agent is the end of the workflow

Then we can run this workflow to get answer for our question this way:
![[2 - Images/LangGraph/Screenshot 4.png]]

Here the Answer agent is dependent on the Retriever one (because it is using the ‘retrieved_docs’ key of the state which is prepared by the Retriever).