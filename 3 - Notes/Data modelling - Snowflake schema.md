Tags: [[__Data_Engineering]] [[_Data_modelling]]
#DataEngineering #DataModelling 

# Introduction
A snowflake schema is a variation of star schema where dimension tables are normalized into multiple related tables.

So instead of wide dimensions, you split them into sub-dimensions.

For example, instead of creating one big dimension table like that:
`Dim_Product`  
`| ProductID | ProductName | Category | Brand |`

we split it into:
`Dim_Product  `
`| ProductID | ProductName | CategoryID | BrandID |`

`Dim_Category  `
`| CategoryID | CategoryName |`

`Dim_Brand  `
`| BrandID | BrandName |`
# Pros
- Less redundancy
- Better data integrity
- More storage efficient in some cases
# Cons
- More joins → slower queries
- More complex for analysts
- Harder for BI tools and users