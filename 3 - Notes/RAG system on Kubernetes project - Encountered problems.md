Tags: [[__My_projects]]
#MyProjects 

# Encountered problems
## Learning new concepts
I needed to learn a lot of new things:
- Indexes in a vector database (Milvus)
- Ray Serve (the most difficult one)
- Asynchronous functions in Python
## Making the `answer_agent` function asynchronous
I made the `answer_agent` function asynchronous, so it can run in parallel with other asynchronous functions.

I made it asynchronous by using commands:
```python
loop = asyncio.get_event_loop()
answer = await loop.run_in_executor(...)
```
## Ray Serve app
### Initiating RAG workflow
I needed to make sure that we load LLM only once, when we start the HTTP server, not every time when someone makes a request.
### Kubernetes deployment
I needed to configure the `RayService` CRD to define how to run Ray Service on Kubernetes. I needed to convert my RAG app into a `.zip` file in order to run it.
## Architecture design
I needed to decide where to convert question into an embedding - on the MCP server or in the app with the `LangGraph` workflow.

I have chosen the MCP server to create a clear separation of responsibilities:
- MCP server does all the heavy computations
- Other applications that uses this MCP server do only light computations. They mainly deal with request handling.