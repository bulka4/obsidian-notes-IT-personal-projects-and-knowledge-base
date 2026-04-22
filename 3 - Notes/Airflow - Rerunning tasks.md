Tags: [[__Data_Engineering]] [[_Airflow]]
#DataEngineering #Airflow 

# Introduction
Airflow tracks task states (`success`, `failed`, etc.).  To rerun something, we clear its state → scheduler treats it as “not run” → executes again (we don't need to trigger the DAG again).
# Ways to rerun tasks
## 1. From UI
- Go to DAG → Graph/Grid view
- Select task(s)
- Click “Clear”

Options:
- clear only selected tasks
- include downstream
- include upstream
- include past/future runs

very flexible for partial reruns
## 2. From CLI
We can do the same via command line:
```shell
airflow tasks clear DAG_ID --task-regex "task_name"
```

Examples:
- clear one task
- clear multiple tasks via regex
- add flags:
    - `--downstream`
    - `--upstream`
    - `--start-date / --end-date`
    - `--only-failed`
## 3. Programmatically (API)
- Airflow REST API allows clearing tasks
- useful for automation or external tools
# Rerun only failed tasks
To rerun only failed tasks:
- UI - Filter tasks by “failed” and clear their state.
- CLI - Select only failed tasks to clear their state by using the `--only-failed` flag