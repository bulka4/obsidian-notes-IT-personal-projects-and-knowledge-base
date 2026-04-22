Tags: [[__DevOps]], [[__Infrastructure_Engineering]], [[_Docker]] 
#DevOps #InfrastructureEngineering #Docker 

# Introduction
We can assign how many resources a container can use:
```bash
docker update --cpus="1.0" --memory="2g" --memory-swap="2g" <container-name>
```