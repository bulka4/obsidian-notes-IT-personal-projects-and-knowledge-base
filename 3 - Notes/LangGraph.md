Tags: [[__Machine_Learning_Engineering]]
# Introduction

Official documentation and tutorial: [langchain-ai.github.io/langgraph](https://langchain-ai.github.io/langgraph/concepts/why-langgraph/).

LangGraph is a tool for AI agents orchestration. For example it enables creating a workflow where:

· We use multiple LLMs

· Allow LLMs to use additional tools

· Add memory from conversations

· Add steps where human can check and approve agent actions

# Multi-agent orchestration

We can use LangGraph for multi-agent orchestration where multiple tasks performed by multiple agents.

Here is how it works:

· Each agent takes as an input the state argument, which is a dictionary, and modifies it

· An agent is dependent on another agent, if it is using state’s key created by the other agent

· We can run multiple agents in parallel if they are not dependent on each other

· Each agent only runs once all its dependencies (parent nodes) produced their outputs

For example, we can create a workflow using two agents and LangGraph like shown below.

One ‘Retriever’ agent is performing a semantic search using a vector database. It finds relevant documents, similar to the given question:
![[2 - Images/LangGraph/Screenshot 1.png]]

This agent:

· Takes as input the state dictionary

· Reads a query (question) from it

· Add a new key to the state about retrieved relevant documents

Second ‘Answer’ agent is generating an answer to a question using documents found by the ‘Retriever’ agent before:
![[2 - Images/LangGraph/Screenshot 2.png]]

This agent:

· Takes as input the state dictionary

· Reads from it information about the documents retrieved by the Retriever agent

· Generates an answer

· Modifies the state such that it contains now only the ‘answer’ and ‘retrieved_docs’ keys

Then we specify the workflow for those agents like here:
![[2 - Images/LangGraph/Screenshot 3.png]]

This indicates that:

· The initial input will go to the Retriever agent

· The state dictionary prepared by the Retriever agent (with a new ‘retrieved_docs’ key) will be an input for the Answer agent

· Output from the Answer agent is the end of the workflow

Then we can run this workflow to get answer for our question this way:
![[2 - Images/LangGraph/Screenshot 4.png]]

Here the Answer agent is dependent on the Retriever one (because it is using the ‘retrieved_docs’ key of the state which is prepared by the Retriever).

# Using tools by LLMs

LLMs instead of giving answer to a question straight away, can indicate which tool to use and with which parameters.

When LLM says to use a tool, then we can use this answer to use the tool with parameters specified by LLM.

Then output from this tool is fed back to the LLM and LLM generates the final answer using the result from the tool.

There are different ways to achieve this result which are described below.

## Question instructions

We can construct a question to LLM in such a way, that we indicate that LLM can either provide an answer straight away or it can tell which tools should be used and with which parameters.

For example we can create a question like this:
![[2 - Images/LangGraph/Screenshot 5.png]]

To make sure that LLM will provide a properly structured answer to such a question, we should use instruction tuned LLMs. They are trained specifically to answer such a questions.

## Built-in tool support

There are tools which provide LLMs with built-in support for using tools. When creating an object  for using LLM, we can call a function to let this LLM know what tools are available.

This LLM is trained in such a way that it can decide whether or not to use a tool and with which parameters. When it decides to use a tool, it provides properly structured response.

In this case when providing a question to such a LLM, we don’t need to tell it how the answer should look like and what tools are available, it already knows it.

Below is an example of how we can let LLM know what tools are available and how the response from this LLM might look like:
![[2 - Images/LangGraph/Screenshot 6.png]]
