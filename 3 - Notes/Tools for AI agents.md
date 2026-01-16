Tags: [[_AI_agents]]
#AIAgents

# Introduction
LLMs instead of giving answer to a question straight away, can indicate which tool to use and with which parameters. Then, we can:
- Use that tool with specified parameters
- Fed the output from that tool back to the LLM
- LLM generates the final answer using the result from the tool

There are different ways to achieve this result which are described below.
# Instruction tuned LLMs
As explained here - [[Instruction tuned LLMs]], we can use LLMs which are trained specifically to follow provided instructions. 

We can use such an LLM to get answer in a proper format indicating which tool to use and with which parameters.
## Question instructions
We can construct a question to LLM in such a way, that we indicate that LLM can either provide an answer straight away or it can tell which tools should be used and with which parameters.

For example we can create a question like this:
![[2 - Images/LangGraph/Screenshot 5.png]]

To make sure that LLM will provide a properly structured answer to such a question, we should use instruction tuned LLMs. They are trained specifically to answer such a questions.
# Built-in tool support
There are tools which provide LLMs with built-in support for using tools. When creating an object for using LLM, we can call a function to let this LLM know what tools are available.

This LLM is trained in such a way that it can decide whether or not to use a tool and with which parameters. When it decides to use a tool, it provides properly structured response.

In this case when providing a question to such a LLM, we don’t need to tell it how the answer should look like and what tools are available, it already knows it.

We can use for example LangChain for that purpose as described here - [[LangChain - Integrating LLMs with tools]].
# MCP
MCP can be used to enable AI agents to use different tools. More information about that can be found here - [[Tools for AI agents - MCP]].
# Examples
Below are common examples of tools that are used by AI agents with links to learn more about them:
- Semantic search with vector databases - [[Vector databases - Semantic search|link]] 