Tags: [[__Data_Engineering]]

# Introduction
We can use snapshots in order to create slowly changing dimensions type 2. We are defining snapshots in a YAML file. 

For example, in the below snapshot we are creating snapshot in such a way that we will create a new record everytime values in the specified columns changes.

If the clients table have the following columns:
clientID | clientName | clientCountry

The output snapshot will have the following columns:

scd_id | clientID | clientName | clientCountry | valid_from | valid_to
![[2 - Images/dbt benefits/Screenshot 3.png]]

#DataEngineering 