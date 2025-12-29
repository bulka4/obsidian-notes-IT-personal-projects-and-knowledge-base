Tags: [[_My_projects]]
#MyProjects 

# Introduction
In the RAG app project - [[RAG app project|link]], we are creating 3 different Helm charts:
- MCP Server
- Prepare Milvus db
- Ray Service

All the Helm charts uses a secret for authentication to ACR when pulling a Docker image. This secret will be created using Service Principal credentials.

Also pods created by those charts can be mounted to Azure File share (depending on the value of the scriptsMounting.enabled parameter).

Values.yaml file for all the charts will be created by Terrafom as described in the ‘Terraform section’. Terraform will insert into them proper values about created Azure resources.
# Mounting apps files through Azure File share
**Why to use mounting**:  
In all the charts, we can mount to AKS pods Azure File share containing our application files which we want to run in pods.

This way we can easily change code running in Pods. We just make changes in code, upload new files to the File share and restart a pod. We don’t need to rebuild the entire image.

**How to use mounting**:
- Enable mounting - In order to enable mounting, when installing Helm charts, we need to set up the scriptsMounting.enabled parameter to true.
- Upload file to File share – We need to upload app’s files to a folder in File share. Name of that folder is specified by the scriptsMounting.volumePath chart parameter.
# Common chart
This chart is saved in the helm_charts/common folder. It creates resources used by multiple other charts:
- acr-secret.yaml - Secret for pulling images from ACR
- sa-secret.yaml - Secret for accessing Storage Account where we keep mounted File share with apps' files  
- pvc.yaml - PVC and PV used for mounting Azure File share with apps' files
# MCP Server chart
This chart is saved in the helm_charts/mcp_server folder.

It deploys MCP Server (as a deployment) with a tool for semantic search which will be used by the Agent.

There is also a service linked to this deployment.

Before we install this chart, we need to install the chart from the helm_charts/prepare_milvus_db folder first.

We can mount File share with apps’ files to created pods as described in the ‘Mounting apps files through Azure File share’ section above.
# Prepare Milvus db chart
This chart is saved in the helm_charts/prepare_milvus_db folder.

It installs the following resources:
- Pods running standalone Milvus db – It is installed as a subchart
- Runs a Python script which prepares sample data in Milvus db

Milvus is a vector db containing documents and their embeddings used by the MCP tool for semantic search.

Release name of this chart determines name of the service used by Milvus, and that determines a DNS name of the Milvus server used for connecting to Milvus.

We can mount File share with apps’ files to created pods as described in the ‘Mounting apps files through Azure File share’ section above.
# Ray Service chart
This chart is saved in the helm_charts/ray_service folder.

It deploys a RayServicve resource which creates a Ray cluster and runs on it the Ray Serve app serving RAG LangGraph workflow as Rest API.

It starts a proxy which listens for clients’ requests and worker processes for Ray Serve deployment replicas which handles requests.

There is also a service linked to the Ray Head pod. On that pod we are running proxy so we can use this service (its name or external IP) in order to make requests to our Rest API.

We can mount File share with apps’ files to created pods as described in the ‘Mounting apps files through Azure File share’ section above.