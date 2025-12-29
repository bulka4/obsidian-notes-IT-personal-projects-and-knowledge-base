Tags: [[__Machine_Learning_Engineering]]

# Introduction
We can use Python to get information about different runs. Below is example of how to do this based on an experiment name:
![[2 - Images/MLflow/Screenshot 7.png]]

In the search_runs function we have different options for querying runs data, for example we can sort results on a start time of a run in a descending order:
![[2 - Images/MLflow/Screenshot 8.png]]

The ‘runs’ variable is a DataFrame with information about runs. It contains such a columns as:
- Run ID
- Experiment ID
- Status
- Start and End Time
- Tags
- Params
- Metrics

We can use this data to find the run ID which we are looking for.

#MLEngineering 