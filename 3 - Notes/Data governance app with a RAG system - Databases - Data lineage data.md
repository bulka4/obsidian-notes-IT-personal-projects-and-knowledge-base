Tags: [[__My_projects]]
#MyProjects 

# Introduction
Data lineage data is stored in the MongoDB database which is used by the data governance backend ([[Data governance app with a RAG system - Data governance backend|link]]) and it is prepared by the metadata extraction pipeline ([[Data governance app with a RAG system - Metadata extraction pipeline|link]]).
# Deployment
MongoDB database for this data is deployed using the `helm_charts/mongo_db` Helm chart.
# Improvements
We could use a SQL database or a graph database would be even better ([[_Graph_databases|link]]). It would make it easier to answer such questions as for example:
> What are the tables dependent (directly or indirectly) on the `Customers` table?