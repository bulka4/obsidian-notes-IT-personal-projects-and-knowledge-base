Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
Schema definition / validation formats are formats used to describe the structure, types, and rules of data. 

Their purpose is to validate data, enforce contracts between systems, and detect incompatible changes in data formats.

The workflow is like this:
- we read some data
- using a Schema definition / validation format we validate this data (check whether it contains all the fields with correct types)
- Through an error if validation fails (there are some missing or unexpected fields, data types are incorrect)

Example Schema definition / validation formats:
- JSON schema - [[Software Engineering - JSON schema|link]] 