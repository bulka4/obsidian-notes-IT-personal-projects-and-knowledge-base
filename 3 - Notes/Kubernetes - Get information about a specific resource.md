Tags: [[__Cloud]], [[__DevOps]], [[__Distributed_computing]], [[__Infrastructure_Engineering]]
#Cloud #DevOps #DistributedComputing #DataEngineering 

# Introduction
To get a specification of a specific resource in YAML format, we can use this command:
```bash
kubectl get <resource-type> <resource-name> -o yaml
```

To get values for a specific key from the YAML manifest of a resource, for example  `spec.tolerations`, we can use the command:
```bash
kubectl get … -o jsonpath=’{.spec.tolerations}’
```
