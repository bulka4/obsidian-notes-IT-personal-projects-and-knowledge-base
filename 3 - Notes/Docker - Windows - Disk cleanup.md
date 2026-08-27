Tags: [[__DevOps]], [[__Infrastructure_Engineering]], [[_Docker]] 
#DevOps #InfrastructureEngineering #Docker 

# Docker prune
- Delete Docker data (images, volumes, cache):
```bash
docker system prune --all --volumes
```
- More about cleaning up a disk on windows - [[Windows - Cleaning up disk]]
# Delete vhdx file
Sometimes, on Windows, using `docker prune` might not release disk space or it doesn't work because we don't have any disk space left. Then, what we can do is:
- close docker desktop
- shutdown wsl - run in terminal: `wsl --shutdown`
- Delete the file (Docker virtual disk): `C:\Users\mbulka\AppData\Local\Docker\wsl\disk\ext4.vhdx`