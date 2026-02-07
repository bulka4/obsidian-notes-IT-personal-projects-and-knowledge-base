Tags: [[_Git]] [[_Kubernetes]]
#Git #Kubernetes 

# Introduction
When using git-sync to clone code to a folder which is mounted, then we can get an error that git-sync doesn't have permissions to save code in that folder.

Permissions in the pod are the same as in the filesystem which is mounted ([[Kubernetes - Volume mounting -  File permissions|link]]) and they can not allow git-sync to save new files in a specified folder.

To solve this problem, we can run an init container in the same pod which runs git-sync. It will change permissions so git-sync get access to a specified folder:
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: git-sync
spec:
  replicas: 1
  selector:
    matchLabels:
      app: git-sync
  template:
    metadata:
      labels:
        app: git-sync
    spec:
      # Init container for setting permissions to the folder where we will be cloning repo. 65533 is UID of the user used in the image
      initContainers:
        - name: init-repo
          image: busybox
          command: ["sh", "-c", "mkdir -p /opt/airflow/dags && chown -R 65533:65533 /opt/airflow/dags"]
          volumeMounts:
            - name: dags
              mountPath: /opt/airflow/dags
      containers:
        - name: git-sync
          image: k8s.gcr.io/git-sync/git-sync:v3.6.0
          volumeMounts:
            - name: dags 
              mountPath: /opt/airflow/dags
      volumes:
        - name: dags
          persistentVolumeClaim:
            claimName: airflow-dags-pvc
```
We need to know the UID of the user used by git-sync (65533 in this example). To learn what is that UID, we can connect into the pod running git-sync (using `exec -it`) and run the `id` command.