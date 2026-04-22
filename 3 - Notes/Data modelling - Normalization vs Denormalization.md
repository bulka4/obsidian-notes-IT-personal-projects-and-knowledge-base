Tags: [[__Data_Engineering]] [[_Data_modelling]]
#DataEngineering #DataModelling 

# Normalization
Normalization is the process of structuring data to reduce redundancy and improve data integrity by splitting data into multiple related tables.

Benefits:
- Avoid duplicate data
- Ensure consistency
- Make updates safe and efficient
# Denormalization
Denormalization is the process of intentionally introducing redundancy by combining tables to improve read performance.

Benefits:
- Reading data is faster because there is less joins to perform
# Example
For example, using normalization we can create separate tables like:
`Customers`  
`| CustomerID | Name | Address |`

`Orders`  
`| OrderID | CustomerID |`

`OrderItems`  
`| OrderID | Product |`

And using denormalization, we can convert it into a single table:
`Orders`
`| OrderID | CustomerName | CustomerAddress | Product |`