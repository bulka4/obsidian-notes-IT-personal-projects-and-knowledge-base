Tags: [[__Data_Engineering]], [[__Distributed_computing]]
#DataEngineering #DistributedComputing 

# Introduction
When we create an init container for driver and executors in the SparkApplication CRD and we want to mount to it a volume, sometimes (for example in case when volume is created from a ConfigMap) we need to mount this volume not only in the init container but also in the driver / executor:
```yaml
apiVersion: "sparkoperator.k8s.io/v1beta2"
kind: SparkApplication
...
spec:
  ...
  volumes:
    - name: spark-conf
      configMap:
        name: spark-conf

  driver:
    ...

    volumeMounts:
      - name: spark-conf
        mountPath: /opt/spark/conf

    initContainers:
      - name: prepare-configs
        ...
        volumeMounts:
          - name: spark-conf
            mountPath: /opt/spark/conf


  # Specify parameters for the Spark Executors' Pods 
  executor:
    ..

    volumeMounts:
      - name: spark-conf
        mountPath: /opt/spark/conf

    initContainers:
      - name: prepare-configs
        ...
        volumeMounts:
          - name: spark-conf
            mountPath: /opt/spark/conf
```