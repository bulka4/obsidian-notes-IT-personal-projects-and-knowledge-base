Tags: [[_Kubeflow]], [[__Machine_Learning_Engineering]]
#Kubeflow #MLEngineering 

# Introduction
KServe is an open-source framework for serving machine learning models on Kubernetes.
# Key Features
1. Kubernetes-native
    - Runs on Kubernetes and leverages its orchestration, scaling, and lifecycle management.
    - Uses Custom Resource Definitions (CRDs) like `InferenceService` to manage ML models declaratively.
2. Model Serving
    - Supports serving models from multiple frameworks: TensorFlow, PyTorch, XGBoost, Scikit-learn, ONNX, and more.
    - Provides HTTP/gRPC endpoints for inference.
3. Autoscaling
    - Integrates with Knative to scale model endpoints up or down automatically based on traffic.
    - Can scale to zero when idle, saving resources.
4. Advanced Inference Features
    - Canary deployments: Gradually roll out new model versions and monitor performance.
    - Explainers: Integrates with frameworks like Alibi for model interpretability.
    - Multi-model support: Deploy multiple versions of models under one service.
5. Extensibility
    - Supports custom predictors, transformers (pre/post-processing), and storage backends.
    - Easily integrates with CI/CD pipelines for ML models.
# Basic Workflow
1. Train a model (e.g., in TensorFlow or PyTorch).
2. Store the model in a storage backend (S3, GCS, PVC, etc.).
3. Create an `InferenceService` YAML specifying the model, runtime ([[Runtime|link]]), and scaling parameters.
4. Apply it to Kubernetes: `kubectl apply -f inference-service.yaml`.
5. KServe handles serving, scaling, and monitoring automatically.
# Limits
## Multi-node distributed inference
If we want to run a multi-node distributed inference (a model and calculations for a single prediction are distributed), then with KServe there will be problems with:
- Starting all the pods at the same time (if one pod is ready while others are not the initialization of a cluster for distributed inference will fail)
- Arranging communication (like NCCL ([[NCCL|link]])) between nodes for distributed computations is tricky
	- For example, DeepSpeed requires to set up proper values for environment variables in each pod like RANK or MASTER_ADDR. This needs to be coordinated across pods while KServe creates pods independently.
# Questions
- 