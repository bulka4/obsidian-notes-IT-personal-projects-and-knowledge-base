Tags: [[_kind]] [[__Cloud]], [[__DevOps]], [[__Distributed_computing]], [[__Infrastructure_Engineering]]
#kind #Cloud #DevOps #DistributedComputing #DataEngineering 

# Introduction
- For deploying resources we can use local Docker images. We need to build an image and load it into kind:
```bash
# Build your image locally
docker build -t my-image:latest .

# Load it into kind
kind load docker-image my-image:latest --name <cluster-name>
```