Tags: [[_Git]] [[_Kubernetes]]
#Git #Kubernetes 

# Introduction
We run git-sync in its own pod which has mounted a PV (Azure File Share in this example). It pulls code from a repo and saves it in this PV which can be then used in other pods.
## PV problem
If we want to be able to mount a PV with pulled code into many pods on different nodes, we need to use RWX access mode ([[Kubernetes - PVC access modes|link]]) in our PV.

Git-sync tries to set up permissions on folders it uses so we need a storage for the PV which supports granting file permissions.

There might be a problem with finding a storage for PV which supports both RWX and setting file permissions. For example:
- Azure disk supports permissions but no RWX
- Azure File Share supports RWX but no permissions
# Solution
As a workaround, we create a pod which runs two containers:
- One 'git-sync' container running git-sync which pulls code and saves it in an ephemeral volume
	- So there is no problem with setting file permissions by git-sync
- Second one, the 'copier' container running a script which copies pulled code into a PV
	- So the code is saved in a PV with RWX access mode and can be mounted into many pods on different nodes

This way we get code saved in a PV with RWX which can be mounted into many pods on different nodes and git-sync doesn't have a problem with file permissions when saving code in an ephemeral volume.
## rsync
The copier container is using 
```bash
rsync -a --delete /source/folder/ /target/folder/
```
command to copy files from the source folder into the target one. `rsync` is efficient as it copies only changes in files, not all the files.

The `--delete` option makes sure that files deleted at the source will get deleted at the target.
# git-sync deployment
```yaml
# This is a deployment running git-sync which pulls code from a repo and saves it in a persistent volume which is then mounted into Airflow pods

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
      containers:
        - name: git-sync
          image: registry.k8s.io/git-sync/git-sync:v4.5.0
          env:
            - name: GITSYNC_REPO
              value: {{ .Values.gitSync.repoURL }}
            - name: GIT_SYNC_BRANCH
              value: {{ .Values.gitSync.branch }}
            # choose as the destination folder a folder which is not the root folder of the mounted volume but a subfloder to avoid
            # permission errors
            - name: GITSYNC_ROOT
              value: /tmp/dags
            - name: GIT_SYNC_WAIT
              value: "60"   # sync interval in seconds
            # Don't set up file permissions, since we are mounting a PV which uses Azure File Share and there are no file permissions
            - name: GIT_SYNC_PERMISSIONS
              value: "0"
            # Run git-sync as a non-root user so we don't get problems with file permissions
            - name: GITSYNC_ADD_USER
              value: "true"
          volumeMounts:
            - name: tmp-dags
              mountPath: /tmp/dags
        # Container which copies code pulled by git-sync into PV
        - name: copier
          image: alpine:3.19
          command:
            - sh
            - -c
            - |
              # Install rsync
              apk add --no-cache rsync
              while true; do
                # Copy file differences from ephemeral clone to RWX PV
                # Remove files at target which are not present at the source anymore
                rsync -a --delete /tmp/dags/<repo-name.git>/apps/airflow/dags/ /opt/airflow/dags/
                sleep 60
              done
          volumeMounts:
            - name: tmp-dags
              mountPath: /tmp/dags
            - name: dags
              mountPath: /opt/airflow/dags
      volumes:
        # Temporary volume for code pulled by git-sync
        - name: tmp-dags
          emptyDir: {}
        # Azure File Share PV where code will be saved and can be mounted to other pods
        - name: dags
          persistentVolumeClaim:
            claimName: airflow-dags-pvc
```