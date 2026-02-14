Tags: [[__DevOps]], [[__Infrastructure_Engineering]], [[_Docker]] 
#DevOps #InfrastructureEngineering #Docker 

# Introduction
In order to change limits for how many resources Docker containers can use, we need to create the `.wslconfig` file in the user folder `C:\Users\<username>`. In that file, we can specify for example:
```bash
memory=8GB
processors=4
```
After modifying that file, we need to run in shell:
```bash
wsl --shutdown
```
and restart Docker Desktop.
# More info
More information about it can be found here - [link](https://learn.microsoft.com/en-us/windows/wsl/wsl-config#configure-global-options-with-wslconfig).
