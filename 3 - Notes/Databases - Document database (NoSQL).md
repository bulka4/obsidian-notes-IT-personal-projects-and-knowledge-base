Tags: [[_Databases]]
#Databases  

# Introduction
- They store documents (usually JSON-like)
# Benefits
- Flexible schema - Good when data changes often (e.g. we add a new field). In NoSQL databases it is much easier to handle than in SQL databases (more info here - [[NoSQL databases - Schema flexibility|NoSQL]] vs [[SQL databases - Schema flexibility|SQL]])
- Easy horizontal scaling ([[NoSQL databases - Horizontal scaling|link]]) - We can easily distribute documents across many machines (easier than in case of SQL). 
- Models well entries with different structure - When entries have different attributes and we use a table, we may end up with a lot of nulls in different columns. It is not a problem when we use documents in a NoSQL database. 
	- For example, if we have a table with products, we might have entries for:
		- Laptops - with attributes like RAM, CPU
		- Books - with attributes like author, pages
# Drawbacks
- Relationships are harder ([[NoSQL databases - Relationships|link]]) - Joining data from multiple documents is slower and code syntax is more complex
- Less efficient aggregations and complex calculations - It can be slower and code can be more complex compared to SQL
- Weaker consistency and transactions
- Data integrity constraints - Setting up those constrains is more limited compared to SQL. Those are constraints specifying that values are e.g. unique, exists in another table (references ([[SQL databases - Referential integrity|link]])), bigger than 0
# Good use cases
- Content management systems
- User profiles
- Product catalogs
- IoT data
- Applications where data structure changes frequently