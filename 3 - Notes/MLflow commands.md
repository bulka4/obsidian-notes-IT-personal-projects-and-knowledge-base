Tags: [[__Machine_Learning_Engineering]], [[_MLflow]]
#MLEngineering #MLflow 

# MLFlow Projects
- Run the current directory as an MLflow Project (using the main entry point)
	>mlflow run .
- Run the project with specific parameter values
	>mlflow run . -P lr=0.01 -P epochs=5
- Run a different entry point (preprocess) from your MLproject file
	>mlflow run . -e preprocess
- Skip Conda/Docker and run using your local Python environment (useful for dev/debugging)
	>mlflow run . --env-manager=local