Tags: [[_Databases]] [[_Graph_databases]]
#Databases #GraphDatabases 

# Introduction
A graph database is useful for data such as:
- social networks
- recommendation systems
- fraud detection
- knowledge graphs
- data lineage

It makes it easy to answer questions like:
- Data lineage - what are the tables dependent (directly or indirectly) on the `Customers` table?
- Social networks - who are all the friends (or friends-of-friends) of `Alice`?
- Knowledge graphs - what are all the topics related to the `IT`, either directly or through intermediate topics?

A graph database lets us traverse a graph by following edges of specified types, for any number of hops, where:
- Edges represent relationships
- Edge of a specific type is an edge representing a specific relation
- Hops mean:
	- 1 hop mean to find only nodes directly connected to one node
	- 2 hops mean to find nodes reachable by traversing two edges (i.e. nodes connected also to nodes found in the hop 1)
	- etc.
# Data lineage
Data lineage data is a data about data transformations happening in a data warehouse (in pipelines, jobs), for example in a SQL database:
- Those are transformations which takes data from multiple source tables, performs transformations on it and saves the result in another table.
- So data lineage data shows us which tables are used to create which other tables.

This data is naturally a graph:
- Nodes - tables, columns, pipelines, jobs
- Edges - "depends on", "reads from", "writes to", "transforms into"
## Example - Finding dependent tables in a graph database vs SQL
If we want to answer for example a question such as:
> Which tables depend on the `Customers` table?

and we store a data lineage data in a SQL database, we would need to perform recursive queries. That's because we would have tables with columns such as:
- `source_table_id` - ID of the table from which we select data
- `script` - Script that populates the target table using data from the source table
- `target_table_id` - ID of the target table which the script populates

so in order to find other tables which are dependent on the `Customers` table (i.e. which tables use data from the `Customers` table), we would need to:
- Make one join to find which tables uses the `Customers` table directly
- Make another join to find which tables uses those tables which uses the `Customers` table directly
- etc.

In a graph database, we just start at the `Customers` node, follows every outgoing `depends on` edge and return all the reachable nodes.