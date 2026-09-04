Tags: [[__My_projects]]
#MyProjects 

# Introduction
Data lineage data is stored in the MongoDB database which is used by the data governance backend ([[Data governance app with a RAG system - Data governance backend|link]]) and it is prepared by the metadata extraction pipeline ([[Data governance app with a RAG system - Metadata extraction pipeline|link]]).
# Data model
Data lineage data has the following schema:
```json
dataLineageSchema:
{
	// A single document of this schema contains a data lineage data for one 
	// table, i.e. showing how a single table
	// is being created.
	
	// Primary key
	dataLineageId: {
		type: Number,
		required: true
	},
	// Name of the given data lineage
	dataLineageName: {
		type: String,
		required: true
	},
	// Nodes which given data lineage graph conists of
	nodes: [nodeSchema]
}

nodeSchema:
{
	// Node's value, e.g. table's name, script's name
	value: {
		type: String,
		required: true
	},
	// Node's type indicating whether it represents a table or a script
	type: {
		type: String,
		required: true
	},
	// LinkedTo indicates to which node this node is linked
	linkedTo: Array,
	// Script's content, if given node represents a script
	script: String,
	// x and y coordinates used to position node on the data lineage graph
	x: Number,
	y: Number
}
```
# Deployment
MongoDB database for this data is deployed using the `helm_charts/mongo_db` Helm chart.
# Improvements
We could use a SQL database or a graph database would be even better ([[_Graph_databases|link]]). It would make it easier to answer such questions as for example:
> What are the tables dependent (directly or indirectly) on the `Customers` table?