Tags: [[_Databases]]
#Databases  

# Features
- Store data in tables
- provide ACID transactions ([[Software Engineering - ACID transactions|link]])
# When to use it
Use them when your data has:
- complex relationships
- strong consistency requirements
- transactions
- structured data
# Benefits
- Good management of relationships ([[SQL databases - Relationships|link]]) - Joining data from multiple tables is efficient and code syntax is easy
- Efficient aggregations and complex calculations - SQL is optimized for this kind of calculations
- Indexing ([[Databases - Indexes|link]]) - We can create indexes to find values in specific columns faster
- Strong consistency ([[Databases - Consistency|link]]) - SQL databases satisfies both read and ACID consistencies
- Transactions - When we have multiple operations to perform, we can make sure that either all of them happen or none happen
- Data integrity constraints - We can make sure that values are e.g. unique, exists in another table (references ([[SQL databases - Referential integrity|link]])), bigger than 0.
# Drawbacks
- Non-flexible schema - When data changes (e.g. we add a new field), in NoSQL databases it is much easier to handle than in SQL databases (more info here - [[NoSQL databases - Schema flexibility|NoSQL]] vs [[SQL databases - Schema flexibility|SQL]])
- Complex horizontal scaling ([[SQL databases - Horizontal scaling|link]]) - Distributing a SQL database across multiple servers is very complicated (for NoSQL databases or object storage it is much easier).
- Doesn't model well entries with different structure - When entries have different attributes, we may end up with a lot of nulls in different columns. 
	- For example, if we have a table with products, we might have entries for:
		- Laptops - with attributes like RAM, CPU
		- Books - with attributes like author, pages
## Good for relations
SQL databases are efficient for handling relations between tables (when column in one table references a column in another table):
- Efficient joins - code syntax is easy and they are fast
- referential integrity ([[SQL databases - Referential integrity|link]])
- Indexes make joins faster
# Questions
- Learn more about:
	- transactions, consistency
	- Data integrity constraints
- Can you explain more Harder handling of highly heterogeneous data?