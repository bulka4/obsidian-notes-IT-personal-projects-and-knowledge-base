Tags: [[__Data_Engineering]] [[_Data_architecture]]
#DataEngineering #DataArchitecture  

# Introduction
A data mart is a subset of a data warehouse designed for a specific business domain or team, like finance or marketing.

Data in a data mart should be simple to use for business owners (mainly data / BI analysts).

Benefits:
- Each data mart is optimized for a specific use case
- Helps to organize data
- Easier to manage governance (e.g. KPIs, ownership, data quality rules) and access permissions
	- Instead of defining KPIs, access permissions etc. per entire company, we define them per data mart (there can be different definitions across different data marts)
- Easy to use by business owners
# Example
Let's assume that a company-wide data warehouse contains:
- Customers
- Orders
- Payments
- Web events
- Inventory
- HR data

Then, we can create data marts like:
- Sales Data Mart
	- orders
	- revenue
	- product performance
- Marketing Data Mart
	- campaigns
	- click-through rates
	- customer acquisition
- Finance Data Mart
	- revenue
	- costs
	- profit metrics
# Questions
- 