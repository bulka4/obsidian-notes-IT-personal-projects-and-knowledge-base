Tags: [[__Data_Engineering]], [[__Distributed_computing]]
#DataEngineering #DistributedComputing 

# Introduction
There is a problem with preparing Spark configs dynamically, that is providing values for configs when we start a pod, for example from a secret.
# Problems
## sparkConf
When using `sparkConf` field in the SparkApplication, we can provide configurations but we can't provide there dynamic values, for example from secrets or env vars.
## Driver pod's entrypoint
In the driver pod created by Spark Operator after deploying SparkApplication, we have an entrypoint like this:
```bash
containers:
  - args:
	- driver
	- --properties-file
	- /opt/spark/conf/spark.properties
	- --class
	- org.apache.spark.deploy.PythonRunner
	- local:///opt/spark/scripts/folder_name/script.py
```

We can check it by using `kubectl -n <namespace> get pod <spark-application-name>-driver -o yaml`.
## Using different folder with configs
When we prepare configs in a different folder, like `/opt/spark/custom_conf` and set the `SPARK_CONF_DIR` env var to that path, Spark still doesn't use those configs.

That's because in the driver's pod container entrypoint there is `--properties-file` used, so it uses only the config file specified there, overwriting the `SPARK_CONF_DIR`.
## Modifying /opt/spark/conf
We can't modify the `/opt/spark/conf` folder by mounting a volume into it because there is already a volume prepared by the Spark Operator mounted into it.

Also, we can't modify this volume which is already mounted as it is read only. In the section below we can read more details about this volume.
### Volume mounted into /opt/spark/conf
In the created driver pod we can see that we have the `spark-conf-volume-driver` volume and mounting:
```yaml
- mountPath: /opt/spark/conf
  name: spark-conf-volume-driver
```

If we use `spec.sparkConfigMap: spark-conf-template` in the SparkApplication, we will have additionally this volume:
```yaml
configMap:
  defaultMode: 420
  name: spark-conf-template
name: spark-configmap-volume
```
and mounting:
```yaml
- mountPath: /etc/spark/conf
  name: spark-configmap-volume
```

We can check it by using `kubectl -n <namespace> get pod <spark-application-name>-driver -o yaml`.

 The `spark-conf-volume-driver` and `spark-configmap-volume` volumes are read-only, even when we mount them into an init container, we can't create or modify files there.

So there is no way to modify `/opt/spark/conf` folder directly. We can't modify the mounted volume or mount another one into the same folder.

We can only modify it by using SparkApplication fields like `spec.sparkConf` or `spec.sparkConfigMap`.
# Debugging tips
- Running `spark.conf.get("spark.sql.catalog.iceberg_catalog", "NOT SET")` shows whether the config is set
- Describe created SparkApplication: `kubectl -n spark get sparkapplication <app-name> -o yaml`
- Describe created driver pod: `kubectl -n spark get pod <spark-application-name>-driver -o yaml`
- Check available fields in the SparkApplication manifest: `kubectl explain sparkapplication.field_1.field_2`
# Potential workarounds
- In the Python script where we run our Spark app we can set up Spark configs using env vars which takes values from secrets..