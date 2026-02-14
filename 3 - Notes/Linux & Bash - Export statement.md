Tags: [[__Infrastructure_Engineering]] [[_Linux & Bash]]
#InfrastructureEngineering #LinuxBash 

# Introduction
In order to make an environment variable available in subprocesses (processes started by another process), we need to use the export statement.

For example, if we want to run a Python script and make env var available for that process we need to run:
```bash
export ENV_VAR=x
# Run the script which will be able to see the ENV_VAR
python3 script.py
```