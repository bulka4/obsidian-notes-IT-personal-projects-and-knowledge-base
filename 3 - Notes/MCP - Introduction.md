Tags: [[__Machine_Learning_Engineering]] [[_MCP]]
#MLEngineering #MCP 

# Introduction
MCP is a protocol which enables one app to use tools (functions) provided by another app. It is commonly used to enable LLMs to use different tools ([[AI agents - Using tools by an agent|link]]).
# Benefits and use cases
It standardizes the way how to ([[MCP - Benefits, use cases and comparison to other approaches|link]]):
- discover what tools are available
- provide descriptions what different tools do and what is an input for them
- how tools are invoked
- how tool results are structured

Thanks to the fact that it standardizes those functionalities, we don't need to implement them on our own.

One of the main applications on MCP is to provide tools to use for LLMs.
# MCP componentes
There are two components of MCP ([[MCP server and client|link]]):
- MCP server ([[MCP server|link]]) – App where we define different tools which can be used. It is a long-running service that listens to requests and sends back tools' outputs as a response.
- MCP client ([[MCP client|link]]) – App which is using tools from a MCP server
# Official documentation
Official documentation about MCP: [modelcontextprotocol.io](https://modelcontextprotocol.io/docs/getting-started/intro).