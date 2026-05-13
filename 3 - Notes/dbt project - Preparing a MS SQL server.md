Tags: [[__My_projects]] [[__Data_Engineering]]
#MyProjects #DataEngineering 

# Introduction
We are preparing a MS SQL server using Docker. All the files needed for that are in the `mssql_preparation` folder. We have there a following files:
- `Dockerfile-draft` - a draft for preparing the Dockerfile as described in the 'Create a Dockerfile' section here - [[dbt project - App prerequisites|link]].
- `sql_server_start.sh` - That script is starting the MS SQL server and executing the `init.sql` script in it.
- `init.sql` - That script is preparing databases, schemas and tables in that SQL server which will be used for making transformations using dbt.
# Preparing data in the MS SQL server
We need to prepare data which we will be transforming using dbt. That will be done by Docker using the `init.sql` script from this respository. 

This script prepares the following tables:
- `purchase_orders` - with the following columns: `orderID | clientID`
- `purchase_orders_details` - with the following columns: `orderDetailsID | orderID | productID | quantity`
- `clients` - with the following columns: `clientID | clientName | clientCountry`
- `products` - with the following columns: `productID | productName | productCategory`

We create above tables in two different schemas: `system_1` and `system_2` in the `source_systems` database. They represent data coming from two different source systems. 

The `init.sql` script also creates the `dwh` database where we will be creating new tables using dbt.