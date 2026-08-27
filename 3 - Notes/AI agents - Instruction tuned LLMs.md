Tags: [[__Machine_Learning_Engineering]], [[_AI_agents]]
#MLEngineering #AIAgents 

# Introduction
Instruction tuned LLMs are trained specifically to follow provided instructions.

For example, we can tell such a model to:
- Answer question using a specific documentation, for example:
- Formulate answer in a specific way

Below are examples of how we can include instructions in our question.

**Ask to provide answer based on a specific documentation:**
```python
prompt = """
Answer the question based on the following documents:
{context}

Question: {query}
"""
```
**Ask to either answer a question directly or tell user which MCP tool to use and with which parameters:**
```python
prompt = """
You are an assistant that can answer a question directly or tell which tool to use with which parameters.

Available tools:
- add(a: int, b: int) <- Add two numbers
  
Provide a JSON as a response in one of the two available formats:
{
	"action": "answer"
	,"response": "your answer to the question"
}

OR

{
	"action": "use-tool"
	,"tool_name": "tool_name"
	,"parameters": {"a": 1, "b": 2}
}
"""
```
# Materials
Some useful materials about instruction tunning:
- [github.com](https://github.com/ubaidkhan08/Fine-Tuned-Chatbot-Tutorial/blob/main/OPENAI%20Approach/OPENAI%20Fine-tuning.ipynb) 
- [medium.com](https://medium.com/@hermanschutte/how-to-custom-train-and-fine-tune-models-with-the-chatgpt-api-afb796aaf2fe) 
- [medium.com](https://medium.com/@r2consultingcloud/a-step-by-step-guide-to-custom-fine-tuning-with-chatgpts-api-using-a-custom-dataset-54dae6c055ce) 