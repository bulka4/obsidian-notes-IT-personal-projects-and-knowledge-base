Tags: [[__Data_Engineering]]

# Introduction
You can tell dbt which tables you want to build and it will automatically build all the other tables on which this table is dependent in a correct order and it will make sure that none table is built twice.

We can run a single command saying ‘build all tables’ and dbt will build all the tables in a correct order, without building any table twice.

For example let’s say that table2 and table3 are both dependent on table1. dbt helps us avoiding problems such as:
We build table2 while table1 has not been built yet.
We build table1 and table2, and after that we build table1 and table3. The table1 has been built twice.
![[2 - Images/dbt benefits/Screenshot 1.png]]

#DataEngineering 