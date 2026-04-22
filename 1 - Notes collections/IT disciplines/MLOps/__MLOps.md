Tags: [[__MLOps]]
#MLOps 

This is a collection of documents related to MLOps, i.e. a set of practices and tools related to creating, monitoring and updating ML models.

# MLOps tasks, problems and practices
1. [[MLOps - Collaboration]]
2. [[MLOps - Feature engineering]]
	1. [[MLOps - Feature store]]
		1. [[MLOps - Incremental + streaming features]]
		2. [[MLOps - Feature store - Online store for real-time inference]]
		3. [[MLOps - Feature store - Time correctness]]
		4. [[MLOps - Feature store - Metadata, documentation and versioning]]
3. [[MLOps - Model reproducibility]]
	1. [[MLOps - Data reproducibility]]
4. [[MLOps - Model versioning]]
5. [[MLOps - Experiment management (keeping track of how different models perform)]]
6. [[MLOps - CI-CD for ML]]
	1. [[MLOps - CI for ML]]
	2. [[MLOps - CD for ML]]
		1. [[MLOps - Canary & shadow deployment]]
		2. [[MLOps - A-B testing]]
		3. [[MLOps - Monitoring]]
			1. [[MLOps - Model performance monitoring & automatic model update]]
			2. [[MLOps - ML system performance monitoring]]
## Questions
## Other topics
- Scaling
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
# GPU ML computing
1. [[_GPU_ML_computing]]
# ML model inference
[[_ML_model_inference]]
# ML model training
[[_ML_model_training]]