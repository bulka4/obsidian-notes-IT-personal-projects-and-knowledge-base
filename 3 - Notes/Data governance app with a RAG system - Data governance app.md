Tags: [[__My_projects]]
#MyProjects 

# Architecture
## Databases
### Tables documentation and data lineage
As a database for tables documentation and data lineage, I have used already MongoDB (NoSQL database) mostly in order to learn it but it would be better to use a SQL database because:
- Schema will not be changing frequently and each table / column will have always the same fields populated
- We will create tables for documentation about objects like: 
	- databases, schemas, tables and columns
	- data lineage - source and target table, script creating the target table

	There are clear relationships between which SQL database will handle well:
	- We can create foreign keys
	- Joins will be efficient (both calculations and code syntax for performing joins will be efficient)
	- It will ensure referential integrity ([[SQL databases - Referential integrity|link]])
- Indexing ([[Databases - Indexes|link]]) - We can create indexes to find values in specific columns faster
- We can make use of data integrity constraints ([[SQL databases - Data integrity constraints|link]]), e.g. we can specify that column names for one table should be unique.
### Vector database for semantic search
As a vector database for semantic search we use Milvus.
## Collecting metadata from a SQL server
in the `db_preparation` folder there are scripts for collecting metadata from a SQL server:
- Needed for data lineage graphs - what scripts there are in views, procedures and jobs, what are source tables used in those scripts and what is the target table that they populate
- List of tables and views - for which we will be able to create documentation

What to improve:
- Allow for creating plugins for collecting metadata from different types of SQL databases (MySQL, Postgres etc.).