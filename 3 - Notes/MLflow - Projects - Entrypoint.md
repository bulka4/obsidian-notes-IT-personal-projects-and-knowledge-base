Tags: [[__Machine_Learning_Engineering]] [[_MLflow]]
#MLEngineering #MLflow 

# Introduction
An entry point is a parametrized command to run a Python script. We run an entrypoint with specific parameters and it runs the associated command.

That entrypoint's script is related to our ML model, for example for:
- Training models
- Preprocess data
- Run evaluations

Entry points are defined in a MLproject file ([[MLflow - Projects - MLproject file|link]]), for example:
```yaml
name: mlflow-project

docker_env:
	image: mlflow:latest
	build_context: .
	
entry_points:
	preprocess:
		command: "python preprocess.py"
		
	train:
		parameters:
			lr:
				type: float
				default: 0.001
			epochs:
				type: int
				default: 50
		command: "python train.py --lr {lr} --epochs {epochs}"
		
	evaluate:
		parameters:
			model_path:
				type: str
			command: "python eval.py --model {model_path}"
```