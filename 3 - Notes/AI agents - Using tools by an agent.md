Tags: [[_AI_agents]]
#AIAgents

# Introduction
LLMs instead of giving answer to a question straight away, can use some tool first and then provide a final answer based on that tool's results. 

For example, that tool can provide the LLM an information about a weather.
# How LLMs use tools
In order to allow LLMs to use tools to help them to generate an answer, we use a workflow like this:
- LLM generates either:
	- A final answer to a question (don't use any tool)
	- or an answer which indicates to use a tool, which one and with which parameters
- Our application executes a tool and feds the result back to LLM
- LLM generates a final response using the tool's result
# Instruction tuned LLMs
As explained here - [[AI agents - Instruction tuned LLMs|link]], we can use LLMs which are trained specifically to follow provided instructions. 

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
MCP can be used to enable AI agents to use different tools. More information about that can be found here - [[AI agents - MCP tools for agents]].
# Examples
Below are common examples of tools that are used by AI agents with links to learn more about them:
- Semantic search with vector databases - [[Semantic search|link]] 