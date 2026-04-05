Tags: [[__Data_Engineering]]

# Introduction
In dbt we are creating YAML files in which we can specify data quality tests. For example on the below example we are checking if ClientID satisfies the following checks:
Values are unique
There are no null values
Every value have corresponding value in the ‘clients’ table (as it is a foreign key).
![[2 - Images/dbt benefits/Screenshot 2.png]]

#DataEngineering 