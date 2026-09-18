Tags: [[__Cloud]], [[__DevOps]], [[__Distributed_computing]], [[__Infrastructure_Engineering]]
#Cloud #DevOps #DistributedComputing #DataEngineering 

# Introduction
Render a Helm chart into a Kubernetes YAML manifest but don't deploy it:
```shell
helm template test . -f values.yaml
```

Show the **Kubernetes YAML that was actually deployed** for an existing Helm release
```bash
helm get manifest <release-name> -n <namespace>
```