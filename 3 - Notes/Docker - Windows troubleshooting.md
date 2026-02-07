Tags: [[__DevOps]], [[__Infrastructure_Engineering]], [[_Docker]] 

## Wsl related problems
To solve problems when we see an error related to the wsl, below materials and methods might be useful.
## Materials
For running Docker on Windows we are using either wsl 2 or hyper v. Check which option we are using and then when looking for solutions check if they are related to wsl 2 or hyper v.
- [www.reddit.com](https://www.reddit.com/r/docker/comments/1ft6u6f/docker_desktop_unexpected_wsl_error/)
- [www.reddit.com](http://www.reddit.com) – Here we are disabling and enabling windows features what can be also done using the Windows Features UI. We just need to look for ‘windows features’ in the search bar next to the windows logo.
## Solutions
- Reinstall Docker:
- Uninstall it in the Control Panel
- Remove all the files related to Docker:
	- In C:\Users\<YourUsername>\AppData:
		- Roaming\Docker
		- Local\Docker
		- Local\Packages – look for any files containing ‘docker’ in its name
	- C:\Users\<YourUsername>\.docker
- Run the command in a terminal: ‘wsl --unregister docker-desktop’
## Debugging on Linux
- journalctl -xe --unit=docker.service
- systemctl status docker.socket
# Running out of disk space
If we run out of a disk space during building an image, we can delete the C:\Users\<your-user>\AppData\Local\Docker folder.

After that we can start the Docker Desktop and click the ‘Clean\Purge’ option to delete all the Docker data.