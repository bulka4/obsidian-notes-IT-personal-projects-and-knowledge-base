Tags: [[__Data_Engineering]]

# Introduction
Macros are functions which we can use in our SQL queries. For example below we have a macro which is returning a data which is a beginning of a financial year specified number of years ago. It assumes that financial year begins at October. Below is also a query which is using this macro. In dbt we can use Jinja except for SQL which gives us more flexibility.

Macro definition:
![[2 - Images/dbt benefits/Screenshot 10.png]]

Macro usage:
![[2 - Images/dbt benefits/Screenshot 11.png]]

#DataEngineering 