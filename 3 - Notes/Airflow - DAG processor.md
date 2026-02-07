Tags: [[__Data_Engineering]] [[_Airflow]]
#DataEngineering #Airflow 

# Introduction
DAG processor parses DAG files and turns them into DAG objects + task metadata. That metadata is stored in the Airflow metadata database so the scheduler can create task runs.

DAG processor:
1. Scans the DAGs folder
    - Finds all `*.py` files
2. Imports each DAG file
    - Executes the Python code
    - This is why top-level code runs on every parse
3. Extracts DAGs and tasks
    - Builds the DAG structure
    - Reads task definitions, dependencies, params, schedules
4. Serializes DAGs
    - Converts DAGs to JSON
    - Writes them to the metadata DB (`serialized_dag` table)
5. Reports parse errors
    - Syntax errors, import errors, runtime errors during parsing