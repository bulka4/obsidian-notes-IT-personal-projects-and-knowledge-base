Tags: [[_dbt]]
#dbt 

# Introduction
dbt uses a catalog ([[Data storage catalog|link]]) to get metadata about data objects which is used to:
- Resolve `ref()` dependencies
- Detect existing tables
- Apply incremental logic
- Run tests against models
- Build documentation