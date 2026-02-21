Tags: [[__Data_Engineering]], [[__Distributed_computing]]
#DataEngineering #DistributedComputing 

# Introduction
In order to test the Thrift Server running on Kubernetes, we can create another pod from which we will connect to the Thrift Server using Python.

Create a pod:
```bash
kubectl -n <namespace> run python-pod \
  --image=python:3.11 \
  --restart=Never \
  -it -- bash
```

Then, inside the pod:
```bash
pip install pyhive thrift thrift_sasl
python3
```

Then, in the Python interactive shell started by `python3`:
```bash
from pyhive import hive
conn = hive.Connection(host="thrift-server-dns", port=10000)
cursor = conn.cursor()
cursor.execute("SHOW DATABASES")
print(cursor.fetchall())
```
