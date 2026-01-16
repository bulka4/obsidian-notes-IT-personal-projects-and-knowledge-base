Tags: [[__Machine_Learning_Engineering]], [[_LangChain]]
#MLEngineering #LangChain 

# Introduction
LLMs instead of giving answer to a question straight away, can indicate which tool to use and with which parameters. More information about that can be found here - [[Tools for AI agents]].
# Integrating LLMs with tools using LangChain
LangChain can provide LLMs with built-in support for using tools. When creating an object for using LLM, we can call a function to let this LLM know what tools are available.

This LLM is trained in such a way that it can decide whether or not to use a tool and with which parameters. When it decides to use a tool, it provides properly structured response.

In this case, when providing a question to such a LLM, we don’t need to tell it how the answer should look like and what tools are available, it already knows it.

Below is an example of how we can let LLM know what tools are available and how the response from this LLM might look like:
![[2 - Images/LangGraph/Screenshot 6.png]]