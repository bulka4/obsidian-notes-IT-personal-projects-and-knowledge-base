Tags: [[__Data_Engineering]] [[_Data_modelling]]
#DataEngineering #DataModelling 

# Introduction
A star schema is a way of organizing data where there is:
- One central fact table
- Multiple dimension tables connected to the fact table

Dimensions are wide and denormalized, e.g. everything about a product is in one table:
`Dim_Product`  
`| ProductID | ProductName | Category | Brand |`

instead of having separate table for product name, category and brand.
# Pros
- Very fast queries (few joins)
- Simple SQL
- Easy for BI tools (Power BI, Tableau)
- Easy for users to understand
# Cons
- Some data redundancy in dimensions
- Slightly less storage efficient than normalized designs