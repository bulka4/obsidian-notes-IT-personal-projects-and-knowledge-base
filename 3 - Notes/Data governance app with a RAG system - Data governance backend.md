Tags: [[__My_projects]]
#MyProjects 

# Introduction
Data governance backend:
- Serves UI 
- Authenticates / authorizes users

It communicates with:
- Semantic search engine
- RAG system
# Architecture
## Databases
### Tables documentation
As a database for tables documentation, I have used already MongoDB (NoSQL database) mostly in order to learn it.

It would be better to use a SQL database because:
- Schema will not be changing frequently and each table / column will have always the same fields populated
- We will create tables for documentation about objects like: 
	- databases, schemas, tables and columns
	- data lineage - source and target table, script creating the target table

	There are clear relationships between those objects which SQL database will handle well:
	- We can create foreign keys
	- Joins will be efficient (both calculations and code syntax for performing joins will be efficient)
	- It will ensure referential integrity ([[SQL databases - Referential integrity|link]])
- Indexing ([[Databases - Indexes|link]]) - We can create indexes to find values in specific columns faster
- We can make use of data integrity constraints ([[SQL databases - Data integrity constraints|link]]), e.g. we can specify that column names for one table should be unique.
### Data lineage
For data lineage I have also already used MongoDB like for tables documentation.

Here, we can also use a SQL database or a graph database would be even better ([[_Graph_databases|link]]). It would make it easier to answer such questions as for example:
> What are the tables dependent (directly or indirectly) on the `Customers` table?
### Vector database for semantic search
As a vector database for semantic search we use Milvus.
## Collecting metadata from a MS SQL server
in the `db_preparation` folder there are scripts for collecting metadata from a MSSQL server:
- Needed for data lineage graphs - what scripts there are in views, procedures and jobs, what are source tables used in those scripts and what is the target table that they populate
- List of tables and views - for which we will be able to create documentation

It can be later converted into a plugin to allow easily replacing it with other plugins for other databases than MS SQL server.
## Authentication and authorization
We use the Passport library and our own RBAC (with permissions stored in a database) for user authentication and authorization.
# Kubernetes deployment
- App running as a deployment (or use Ray Serve optionally)
- 