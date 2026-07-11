Tags: [[_Databases]]
#Databases  

# Introduction
OLAP describes a type of database workload/application which focus on:
- Large queries over lots of data
- Aggregations and analysis
- Reporting and business intelligence

Example:
```sql
SELECT country, SUM(revenue)
FROM sales
GROUP BY country;
```

Typical OLAP systems:
- Data warehouses
- Columnar databases
- Analytical platforms