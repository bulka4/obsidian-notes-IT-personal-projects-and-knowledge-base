Tags: [[_kind]] [[__Cloud]], [[__DevOps]], [[__Distributed_computing]], [[__Infrastructure_Engineering]]
#kind #Cloud #DevOps #DistributedComputing #DataEngineering 

# Introduction
If we create a Kubernetes service for a pod and want to connect to it from a localhost, we need to use `NodePort` type of a service.

In the service specification `service.yaml` we need to define:
```yaml
type: NodePort
  ports:
    - port: 80          # service port (used inside the cluster)
      targetPort: 8080  # container port
      nodePort: 30080   # node port
```

and in the `kind-config.yaml` we need to define for the control plane:
```yaml
nodes:
  - role: control-plane
	extraPortMappings:
# port for accessing services. We will use nodePort services (like webserver service specified in the helm_charts/airflow/values.yaml)
# which maps containerPort 30080 to the port in containers using the service.
	      - containerPort: 30080
	        hostPort: 8080
	        protocol: TCP
```

Then traffic will go like that:
- host port (port on the host specified in the `kind-config.yaml`) ->
- container port / node port (port in the kind node container, specified in the `kind-config.yaml` as `containerPort` and in the `service.yaml` as `nodePort`) ->
- target port (port in the container running in the kind cluster, specified in the `service.yaml`)