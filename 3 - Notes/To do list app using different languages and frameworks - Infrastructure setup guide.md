Tags: [[__My_projects]]
#MyProjects 

# Setup Vite (HTTP server)
## First time - set up Vite
- Install Node.js (`v18.17.0`) and npm (`9.6.7`)
- run the command in the project's folder:
  ```bash
  npm create vite@5 .
  ```
  - Choose options:
	  - `React`
	  - `TypeScript + SWC` (SWC is a fast compiler written in Rust that transforms TypeScript/JSX into JavaScript.)
  - Run:
	```bash
	npm install  # install packages from package.json
	npm run dev  # Start the Vite development HTTP server
	```
## Every time - start HTTP server
After doing this, every time we want to run the HTTP server, we just run:
```bash
npm run dev
```
# Starting the kind cluster
- Start Docker engine
- Start the kind cluster:
```bash
# Run this from the repo root folder
kind create cluster --name to-do-app --config kind-config.yaml
```
- Copy the `.kube` folder (usually located at `C:\Users\username`) into the repo root folder (so it can be copied into the image we build in the next step)
- Build and run the image for interacting with kind ([[Data and ML platform project - Docker image for interacting with AKS|link]]):
```bash
# Run this from the repo root folder
docker build -t interacting-kind -f interacting.kind.Dockerfile .
docker run -it --rm interacting-kind bash
```
# Cleanup
How to clean up resources when we are done.

Cleanup of Docker images:
```bash
# remove all containers
docker rm $(docker ps -aq)

# remove all images
docker rmi $(docker image ls -aq)

# remove build cache
docker image prune -a
docker builder prune -a

# remove everything (images, containers, cache, volumes)
docker system prune --all --volumes
```

Delete the kind cluster:
```bash
kind delete cluster --name data-platform
```
# Prepare images
From inside of the image for interacting with Kubernetes:
- Run commands from the `/root/dockerfiles/build_and_load.sh` script on the host (run them outside of the image for interacting with kind. They require to use Docker)
	- It builds Docker images and loads them to kind, so they can be used to run pods