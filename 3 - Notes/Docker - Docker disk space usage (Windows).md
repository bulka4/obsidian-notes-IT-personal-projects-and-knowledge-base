Tags: [[__DevOps]], [[__Infrastructure_Engineering]], [[_Docker]] 

# Introduction
In order to reduce the disk space used by Docker, we need to:
- Go to the Docker Desktop app
- Click on the ‘?’ icon at the top
- Click on ‘Clean / Purge data’

Just deleting docker resources using commands like ‘docker rmi’ or ‘docker prune -a’ doesn’t reduce the disk space used by Docker.

The most disk space is used by this file:
- C:\Users\user\AppData\Local\Docker\wsl\disk\docker_data.vhdx

It contains data about docker resources (images, volumes, caching etc).

#DevOps #InfrastructureEngineering #Docker 