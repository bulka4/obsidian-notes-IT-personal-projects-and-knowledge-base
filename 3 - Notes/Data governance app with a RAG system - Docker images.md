Tags: [[__My_projects]]
#MyProjects 

# Docker images and Dockerfiles
Docker images and Dockerfiles we use:
- `services/semantic_search/Dockerfile` - For image for semantic search, that is:
	- Downloading a model from Hugging Face and saving it in the ONNX format
	- Loading and using the saved ONNX model in a Python script
	- Running FastAPI routes
	- Running a MCP server
	- Interacting with Milvus
# Building images
We can build images and load them to kind so they can be used in pods using the `bash/build_and_load_images.sh` script (we need to run it in the container for interacting with kind ([[Data governance app with a RAG system - Docker image for interacting with kind|link]])).