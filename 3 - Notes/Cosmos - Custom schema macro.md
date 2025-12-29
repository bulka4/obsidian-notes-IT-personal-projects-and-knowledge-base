Tags: [[__Data_Engineering]]

# Introduction
The purpose of the custom_schema.sql macro is to create models in schemas specified in the dbt_project.yml file. Otherwise when running dbt with cosmos it might use as a schema name a name obtained by contatenating schema names from profiles.yml and dbt_project.yml.

#DataEngineering 