Tags: [[__Infrastructure_Engineering]] [[_Linux & Bash]]
#InfrastructureEngineering #LinuxBash 

# At the same time
We can run many commands which will be started one by one immediately, without waiting for them to finish. So they will both run at the same time:
```bash
command1 & command2
```
# Sequentially
We can run commands sequentially, such that before we start the next command, we wait for the previous one to complete:
```bash
command1 && command2
```