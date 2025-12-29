Tags: [[__Data_Engineering]]

# Normalization vs Denormalization

# Star schema

# Snowflake schema

# Fact and dimension tables

# Data marts

# Database layers

We can structure data in a database in such a way that we create layers, where:

· Each layer is a group of datasets with specific characteristics

· Data from one layer is used to create data in another layer

For example we might a structure like this:

· **Source system db** – The first data layer. One db per source system, called for example 01_System_1, 01_System_2.

· **02_Transformed db** – The second layer consisting of transformed data. There will be a separate schema per each source system, called for example System_1, System_2.

· **DWH** – The third layer with data for reports.

The DWH db should have the following schemas:

· **Common** – for common dimensions

· **Reference** – for reference data

· **Business function specific schemas** – for every business function (operations, finance etc) there will be a separate schema.
# Data mesh
# Slowly changing dimensions