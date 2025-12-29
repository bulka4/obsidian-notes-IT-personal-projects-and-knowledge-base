Tags: [[__Machine_Learning_Engineering]]

# Introduction

Those notes are about IT tools used for building AI agents. Related notes about machine learning theory (NLP) can be found in the ‘machine learning > NLP > NLP notes’ file.

# MCP

Official documentation about MCP: [modelcontextprotocol.io](https://modelcontextprotocol.io/docs/getting-started/intro).

MCP enables applications to use different tools which we create. It is a protocol which allows one app talk to the other app which provides tools to be used.

It is designed mainly to enable LLMs using different tools.

There are two components of MCP:

· MCP server – App where we define different tools which can be used by MCP clients

· MCP client – App which is using tools from a MCP server

**Example use case**

Let’s assume that we have a vector database which contains documents and their vector embeddings which represent a meaning of those documents.

A MCP server can provide a tool for semantic search, that is a tool which takes as an input a question, and returns documents from a vector database relevant to this question (with a similar meaning).

It is done by converting a question into a vector embedding, and finding vectors in a vector db which are the most similar to the input vector.

A MCP client can be an app which takes a question from a user, uses the MCP tool to find relevant documents, provides as an input to LLM a question together with relevant documents, and LLM generates an answer.

**More information**

More information about FastMCP, which is a Python framework for workin with MCP, is in the ‘ml engineering > MCP > MCP - FastMCP notes’ documentation in the knowledge base.

# Instruction tuned LLM

Instruction tuned LLMs are trained specifically to follow provided instructions.

For example, we can tell such a model to:

· Answer question using a specific documentation, for example:

· Formulate answer in a specific way

Below are examples of how we can include instructions in our question.

**Ask to provide answer based on a specific documentation:**
![[2 - Images/AI agents/Screenshot 1.png]]

**Ask to either answer a question directly or tell user which MCP tool to use and with which parameters:**
![[2 - Images/AI agents/Screenshot 2.png]]

# Semantic search

Semantic search is about finding text with a similar meaning to the given, another text.

Semantic search is performed this way:

· Take a question

· Convert the question into a vector embedding. That vector represents the meaning of the question.

· Compare our question’s vector to other vectors (created from other sentences) and find the most similar ones. If vectors are similar, that means that sentences represented by those vectors are similar.

We can use for semantic search vector dbs:

1. **Create a vector db**

· Convert documents into vector embeddings using LLM

· Save embeddings together with corresponding text in a vector db

2. **Find documents in a vector db similar to the given question**

· Convert a question into a vector embedding using LLM

· Find in a vector db docs with vectors similar the question’s vector

## Vector dbs

Here is a short description of vector databases. More detailed information can be found in the ‘ml engineering > vector databases’ folder in this knowledge base.

There are two ways how vector dbs can store their data:

· In memory

· On disk

Example tools for creating vector dbs:

· Milvus – Stores data on disk

· FAISS – Stores data only in memory

· Chroma – Can store data in both memory and on disk

## Serving searching vector dbs – Rest API / MCP

If our vector db stores data in memory, then creating it for every question is not practical.

Instead we need to create a long running service which builds a vector db once, and enables other apps to search through this db.

We can create for example a Rest API or MCP server to which other apps can send a question and it will send similar docs from a vector db as a response.

We can create this Rest API on our own or use a vector db which provides such an API, for example Chroma.

Here is an example script of creating our own Rest API where we use FAISS as a vector db which stores data in memory. It consists of two parts.

In the first part we:

· Convert docs into vector embeddings

· Save embeddings in a vector db

· Save vector db in a file
![[2 - Images/AI agents/Screenshot 3.png]]

In the second part we:

· Load the vector db from a file

· Create a Rest API where we find docs similar to a question

Finding similar docs is done in the following way:

· Convert a question into a vector embedding

· Find similar vectors in a vector db
![[2 - Images/AI agents/Screenshot 4.png]]

There are also tools for building vector dbs which provides Rest APIs and which can store data on a disk.

# LangGraph

Official documentation and tutorial: [langchain-ai.github.io/langgraph](https://langchain-ai.github.io/langgraph/concepts/why-langgraph/).

LangGraph is a tool for AI agents orchestration. For example it enables creating a workflow where:

· We use multiple LLMs

· Allow LLMs to use additional tools

· Add memory from conversations

· Add steps where human can check and approve agent actions

More information about it can be found in the ‘LangGraph’ document in the same folder as this document.

# Multi-agent orchestration

Multi-agent orchestration is orchestrating multiple tasks performed by multiple agents.

For example, we can create a workflow where we use multiple agents to answer a question based on available documentation. It works in the following way:

· User ask a question

· The ‘Retriever’ agent converts this question into a vector embedding and retrieves from a vector db documents with similar vector embeddings.

· The ‘Answer’ agent uses the retrieved documents to generate a final answer.

LangGraph can be used for such an orchestration. More information about it can be found in the ‘LangGraph’ document in the same folder as this document.

# Using tools by LLMs

LLMs instead of giving answer to a question straight away, can indicate which tool to use and with which parameters.

When LLM says to use a tool, then we can use this answer to use the tool with parameters specified by LLM.

Then output from this tool is fed back to the LLM and LLM generates the final answer using the result from the tool.

More information about it can be found in the ‘LangGraph’ document in the same folder as this document.