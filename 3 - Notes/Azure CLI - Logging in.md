Tags: [[__DevOps]], [[__Infrastructure_Engineering]]

# Introduction
If logging in using ‘az login’ doesn’t work we might try to run this:
```shell
az account clear
az config set core.enable_broker_on_windows=false
az login
```

#DevOps #InfrastructureEngineering 