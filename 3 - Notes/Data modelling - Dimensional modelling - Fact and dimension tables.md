Tags: [[__Data_Engineering]] [[_Data_modelling]]
#DataEngineering #DataModelling 

# Introduction
In a dimensional modeling ([[Data modelling - Dimensional modelling|link]]), we differentiate two types of tables:
- Fact tables - Tables containing data about events (big tables, for example sales)
- Dimension tables - Tables with attributes describing objects appearing in events (smaller tables, for example about customers)

For example, a fact table can be about sales and have columns like that:
`| ID | date | customerID | productID | amount |`

and dimension table can describe a customer and product objects, providing their attributes:
- customers: `| customerID | customerName | customerCountry |`
- products: `| productID | productName | productPrice |`