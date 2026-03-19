Tags: [[__DevOps]], [[__Infrastructure_Engineering]], [[_Docker]] 
#DevOps #InfrastructureEngineering #Docker 

# Docker prune
- Delete Docker data (images, volumes, cache):
```bash
docker system prune --all --volumes
```
- More about cleaning up a disk on windows - [[Windows - Cleaning up disk]]
# Delete vhdx file
If docker prune doesn't work (because we don't have any disk space left) or when it is not enough:
- close docker desktop
- shutdown wsl: `wsl --shutdown`
- Delete the file: `C:\Users\mbulka\AppData\Local\Docker\wsl\disk\ext4.vhdx`
- 