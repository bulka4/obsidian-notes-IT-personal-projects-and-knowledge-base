Tags: [[__MLOps]]
#MLOps 

This is a collection of documents related to MLOps, i.e. a set of practices and tools related to creating, monitoring and updating ML models.

# MLOps tasks and problems
1. [[MLOps - Collaboration]]
2. [[MLOps - Feature engineering]]
	1. [[MLOps - Feature store]]
3. [[MLOps - Monitoring]]
	1. [[MLOps - Model performance monitoring & automatic model update]]
	2. [[MLOps - ML system performance monitoring]]
4. [[MLOps - Model reproducibility]]
	1. [[MLOps - Data reproducibility]]
5. [[MLOps - Model versioning]]
6. [[MLOps - Experiment management (keeping track of how different models perform)]]
7. [[MLOps - Canary testing - shadow deployment]]
## Questions
## Other topics
- Scaling
- CI/CD for ML
	- When I train models using MLflow and Airflow and save them in MLflow registry (to release them into production), is this a CI/CD?
- integration tests for ML pipelines
	- and other kinds of testing
- Feature stores – centralized storage for reusable, consistent features
- Online vs offline feature consistency – avoiding training/serving skew
- Governance & Compliance
	- Model governance – approvals, audit trails
	- Explainability / interpretability – SHAP, LIME, etc.
	- Fairness & bias detection
	- Regulatory compliance (important in finance, healthcare)
- Security
	- Data security – PII handling, encryption
	- Model security – adversarial attacks, model stealing
	- Access control – who can deploy/train models
- Cost & Resource Management
	- Cost monitoring – training and inference costs
	- Autoscaling strategies
	- Resource optimization (spot instances, batching, etc.)
- Observability (beyond monitoring)
	- Tracing – request-level tracking across services
	- Logging strategies for predictions and features
	- Root cause analysis practices
- Multi-model / System design
	- Ensemble systems
	- Model routing (which model to use when)
	- A/B testing for models
# GPU ML computing
1. [[_GPU_ML_computing]]
# ML model inference
[[_ML_model_inference]]
# ML model training
[[_ML_model_training]]