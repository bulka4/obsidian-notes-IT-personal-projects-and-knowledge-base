Tags: [[__Data_Engineering]]

# Introduction
In the profiles.yml file we can specify different targets, that is different databases where we will be building models. For example here we are specifying two targets called ‘dev’ and ‘prod’:
![[2 - Images/dbt/Screenshot 3.png]]

When we are building models using dbt commands we can specify in which target we want build our models:
```
dbt run --target <target_name>
```

#DataEngineering 