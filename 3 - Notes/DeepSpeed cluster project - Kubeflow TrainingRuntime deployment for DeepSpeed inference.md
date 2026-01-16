Tags: [[_My_projects]]
#MyProjects 

# Introduction
This document describes next steps and plan regarding the DeepSpeed cluster project - [[DeepSpeed cluster project|link]].
# TrainingRuntime CRD
Deploy headless service for the master node first:
```yaml
apiVersion: v1
kind: Service
metadata:
  name: deepspeed-master
spec:
  clusterIP: None
  selector:
    app: deepspeed
  ports:
    - port: 29500
      name: ds-port
```

Then deploy TrainingRuntime CRD which will use that service:
```yaml
apiVersion: training.kubeflow.org/v1alpha1
kind: TrainingRuntime
metadata:
  name: deepspeed-runtime
spec:
  replicas: 2
  template:
	metadata:
      labels:
        app: deepspeed
    spec:
      containers:
        - name: deepspeed
          image: <your-registry>/deepspeed:latest
          command: ["deepspeed"]
          args:
            - "--num_gpus=4"
            - "train.py"
            - "--deepspeed_config"
            - "ds_config.json"
          env:
            - name: MASTER_ADDR
              value: "deepspeed-master"
            - name: MASTER_PORT
              value: "29500"
            - name: WORLD_SIZE
              value: "2" # total number of nodes
            - name: RANK
              valueFrom:
                fieldRef:
                  fieldPath: metadata.annotations['kubeflow.org/rank']
          volumeMounts:
            - name: checkpoint
              mountPath: /mnt/checkpoints
      volumes:
        - name: checkpoint
          persistentVolumeClaim:
            claimName: deepspeed-pvc
	  resources:
		limits:
		  nvidia.com/gpu: 1

```

We use here valueFrom.fieldRef.fieldPath to get value for `RANK` from pod's metadata ([[Kubernetes - Pod metadata|link]]) prepared by Kubeflow.
# Python script
Script which loads a model using DeepSpeed and starts Rest API server using FastAPI and Uvicorn:
```python
import os
import torch
import deepspeed
import torch.distributed as dist
from fastapi import FastAPI
import uvicorn

# ------------------------------------------------
# Distributed init (DeepSpeed handles process group)
# ------------------------------------------------
rank = int(os.environ["RANK"])
world_size = int(os.environ["WORLD_SIZE"])

dist.init_process_group(backend="nccl")

# ------------------------------------------------
# Load model
# ------------------------------------------------
class MyModel(torch.nn.Module):
    def __init__(self):
        super().__init__()
        self.linear = torch.nn.Linear(10, 1)

    def forward(self, x):
        return self.linear(x)

model = MyModel().cuda()

# ------------------------------------------------
# Initialize DeepSpeed (ZeRO etc.)
# ------------------------------------------------
model_engine, _, _, _ = deepspeed.initialize(
    model=model,
    model_parameters=model.parameters(),
    config="ds_config.json",
)

# ------------------------------------------------
# FastAPI ONLY on rank 0 node
# ------------------------------------------------
if rank == 0:
    app = FastAPI()

    @app.post("/predict")
    def predict(x: list[float]):
        with torch.no_grad():
            tensor = torch.tensor(x).cuda()
            output = model_engine(tensor)
            return {"result": output.item()}

    if __name__ == "__main__":
        uvicorn.run(app, host="0.0.0.0", port=8000)

else:
    # Other ranks must stay alive. This command will wait for other processes to reach this line of code, and rank 0 will never do that.
    dist.barrier()
```
# GPU + NCCL
Make sure to set up env vars:
```shell
NCCL_DEBUG=INFO
NCCL_SOCKET_IFNAME=eth0
NCCL_IB_DISABLE=1
```