Tags: [[__Machine_Learning_Engineering]] [[_MLflow]]
#MLEngineering #MLflow 

# Introduction
A MLproject file is a YAML file which describes:
- Project name
- Environment (conda, docker, or system) ([[MLflow - Projects - Environment preparation|link]])
- Entry points (commands for running scripts) ([[MLflow - Projects - Entrypoint|link]])
- Parameters (if any)

It can look for example like that:
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