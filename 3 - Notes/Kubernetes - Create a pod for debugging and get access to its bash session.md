Tags: [[__Cloud]], [[__DevOps]], [[__Distributed_computing]], [[__Infrastructure_Engineering]]
#Cloud #DevOps #DistributedComputing #DataEngineering 

# Introduction
For debugging, we can create a pod, connect into it (using `exec -it`) and run from it commands for testing different things, for example networking, file permissions, how commands work.

We can use for that for example the busybox – publicly available Docker image or our own image which we want to test.

We can use this command to create a pod, get access to a bash session in it and delete the Pod after exiting that bash session:
```bash
kubectl run -rm -it <pod-name> --image=your-docker-image -- /bin/bash
```
Or use YAML manifest:
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: debug
  namespace: <namespace>
spec:
  containers:
    - name: example
      image: busybox
      command: ["sh", "-c"]
      args: ["sleep 3600"]
      volumeMounts:
        - name: data-volume
          mountPath: /data
  volumes:
    - name: data-volume
      persistentVolumeClaim:
        claimName: my-pvc
  restartPolicy: Never
```