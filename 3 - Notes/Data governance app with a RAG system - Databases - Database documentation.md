Tags: [[__My_projects]]
#MyProjects 

# Introduction
Database documentation (about tables, columns, scripts, etc.) data is stored in the MongoDB database which is used by the data governance backend ([[Data governance app with a RAG system - Data governance backend|link]]) and it is prepared by the metadata extraction pipeline ([[Data governance app with a RAG system - Metadata extraction pipeline|link]]).
# Deployment
MongoDB database for this data is deployed using the `helm_charts/mongo_db` Helm chart.
# Improvements
## Using SQL
As a database for database documentation, I have used already MongoDB (NoSQL database) mostly in order to learn it.

MongoDB data models are defined in the `data_governance_backend/mongo_models` folder.

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