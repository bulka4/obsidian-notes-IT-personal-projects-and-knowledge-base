Tags: [[_My_projects]]
#MyProjects 

# Hive
We use a small image containing only Hive Metastore, without HiveServer2 and other, unnecessary libraries and jars which uses a lot of memory.
# To do
## PostgreSQL
- Run `schematool -dbType postgres -initSchema` in the hive pod to prepare database
- Fix the issue with exit code 137 appearing