Tags: [[__Machine_Learning_Engineering]] [[_MLflow]]
#MLEngineering #MLflow 

# Introduction
We can assign an alias (our chosen name, like a tag) to a registered model ([[MLflow - Registry|link]]) version.

Key features:
- One model version can have multiple aliases.
- Aliases are stored as pairs `alias_name:model_version` for each model:
  ```python
	Model_1 -> aliases={'alias_11': '1', 'alias_12': '2'}
	Model_2 -> aliases={'alias_21': '1', 'alias_22': '2'}
  ```
- For each model, each alias name is unique (can be assigned only to one model version). 
- There can be the same alias name for different models.
- If we have an alias name assigned to one model version and then we assign it to another model version, the previous version automatically looses that alias (we don't need to remove it manually and there will be no duplicates).
