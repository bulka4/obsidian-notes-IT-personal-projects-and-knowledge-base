Tags: [[__DevOps]], [[__Infrastructure_Engineering]], [[_Docker]] 
#DevOps #InfrastructureEngineering #Docker 

## Wsl related problems
To solve problems when we see an error related to the wsl, below materials and methods might be useful.
## Materials
For running Docker on Windows we are using either wsl 2 or hyper v. Check which option we are using and then when looking for solutions check if they are related to wsl 2 or hyper v.
- [www.reddit.com](https://www.reddit.com/r/docker/comments/1ft6u6f/docker_desktop_unexpected_wsl_error/)
- [www.reddit.com](http://www.reddit.com) – Here we are disabling and enabling windows features what can be also done using the Windows Features UI. We just need to look for ‘windows features’ in the search bar next to the windows logo.
## Solutions
- Run:
```bash
# Restart wsl
wsl --shutdown
# Unregister docker-desktop
wsl --unregister docker-desktop
```
- WSL Network Reset. Open powerShell as admin and run:
	```bash
	netsh winsock reset
	netsh int ip reset all
	```
	and restart PC
- Above two solutions are usually enough
- Uninstall Docker in the Control Panel
- Remove all the files related to Docker:
	- C:\Users\<YourUsername>\.docker
	- In C:\Users\<YourUsername>\AppData:
		- Local\Docker
		- Local\Packages – look for any files containing ‘docker’ in its name
		- Roaming\Docker
	- search for other 'docker' files in the AppData/Local folder
- Optional. Open powerShell as admin and run:
	- Delete Docker’s Network Settings:
	```bash
	# This one also removes saved wi-fi passwords
	netcfg -d
	```
	and restart PC
## Debugging on Linux
- journalctl -xe --unit=docker.service
- systemctl status docker.socket
# Running out of disk space
If we run out of a disk space during building an image, we can delete the C:\Users\<your-user>\AppData\Local\Docker folder.

After that we can start the Docker Desktop and click the ‘Clean\Purge’ option to delete all the Docker data.