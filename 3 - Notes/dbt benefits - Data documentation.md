Tags: [[__Data_Engineering]]

# Introduction
dbt generates a website with data dictionary like it is shown below. Tables and columns descriptions are defined in YAML files like it is shown in the previous slide.
![[2 - Images/dbt benefits/Screenshot 4.png]]

dbt generates also data lineage visualizations on the same website with data dictionary.
![[2 - Images/dbt benefits/Screenshot 5.png]]

If we run dbt in Airflow using cosmos then we will also see data lineage in an Airflow graph. If we click on a specific task we can see the code used for building a table and logs. In that Airflow graph we can have also other tasks than dbt transformations.
![[2 - Images/dbt benefits/Screenshot 6.png]]

#DataEngineering 