Tags: [[__MLOps]]
#MLOps 

# Introduction
A feature store helps with:
- Documenting, versioning and searching through features
- Creating a data lineage showing how features are calculated (lineage for a single feature, not the entire table)

Documentation can include:
- Who is an owner
- How frequently a feature is being refreshed

Metadata is required when creating a feature.

That allows to search through an existing features and find out whether a feature which we need already exists so we can reuse it.

A feature store also helps with versioning features.
# Questions
- The main goal of documenting is to search through an existing features and find out whether a feature which we need already exists so we can reuse it. I can create exactly the same documentation on dbt and is a feature store and search through it the same way. What is a difference?