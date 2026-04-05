Tags: [[__Data_Engineering]]
#DataEngineering 

# Introduction
Data quality tests check whether data is good and usable. In contrast to schema validation ([[Data Engineering - Schema validation|link]]), they don't focus on data structure but on values in tables.

For example, data quality tests can check:
- No duplicates for values which should be unique
- Valid numeric ranges (e.g. 0 < age < 130)
- Referential integrity (foreign keys match)
- Freshness (data is up to date)
- Completeness (no unexpected nulls)
# dbt
When using dbt, unit tests can be used for data quality tests ([[dbt benefits - Data quality tests (unit tests)|link]]).