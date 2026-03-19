Tags: [[__Machine_Learning_Engineering]], [[_MLflow]]
#MLEngineering #MLflow 

# Introduction
The `mlflow run <directory> [options]` command is used to run a MLflow project. 

We need to provide for `<directory>` a path to the directory containing the MLflow project (the `.` value means to use the current directory).

We have the following options there:
- `-P param_1=x_1 -P param_2=x_2` - Run the project with specific parameter values for entrypoints (those are values for the `parameters` section in the `MLproject` file)
- `-e entrypoint_name` - Run a specific entrypoint defined in the `MLproject` file
- `--env-manage <option-name>` - Choose Python environment. Options include:
	- `local` - Use local environment
	- `virtualenv` - Create a `venv`
	- `conda` - Create a Conda environment