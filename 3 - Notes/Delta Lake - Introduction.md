Tags: [[__Data_Engineering]], [[Object storage]] 
#DataEngineering #ObjectStorage 

# Introduction
Delta lake is a storage framework that adds useful functionalities for working with data files. Main benefits are:

· **Enabling SQL** – Delta lake stores tables metadata like Hive and enables running SQL queries on them. It is also more efficient than Hive.

· **ACID transactions** – Delta lake assures ACID when performing data transformations.

· **Time travel (data versioning)** – It keeps track of what changes happen to data and we can go back to the previous version of a table, before we made some changes.

· **Provides useful functions for working with data** – functions such as:
	o Merge (combines insert, update and delete in one operation)
	o Functions helping creating Slowly Changing Dimensions

· **Protects data from corruption** – Our table is a folder consisting of multiple files. Without Delta lake we might save a new file in that folder with different columns or data types in columns and that will break the table. Delta lake makes sure problems like that don’t happen.

#DataEngineering #ObjectStorage 