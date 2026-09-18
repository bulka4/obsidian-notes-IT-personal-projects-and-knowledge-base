Tags: [[__My_projects]]
#MyProjects 

# Introduction
Data governance backend:
- Serves UI 
- Authenticates / authorizes users

It communicates with:
- Semantic search engine
- RAG system
# Kubernetes deployment
## Dependencies
Before we deploy the app, we need to satisfy the following requirements:
- Run the metadata extraction pipeline (more info here - [[Data governance app with a RAG system - Metadata extraction pipeline|link]])
	- It will extract metadata about tables and scripts from the source MS SQL Server which will be used by the app (e.g. it prepares a list of tables for which we can create documentation from the app)
- Run the embedding ingestion service (more info here - [[Data governance app with a RAG system - Embedding Ingestion Pipeline and Service|link]])
	- It will be ingesting vector embeddings into a vector store every time we create a table description in the Data Governance app
- Install the Redis Helm chart:
	- Redis is used for caching in this backend
  ```bash
	# Execute below commands from the helm_charts/redis folder
	helm dependency build
	helm -n semantic-search install redis . &
  ```
## Data Governance Backend deployment
Once the dependencies are prepared, we can deploy the Data Governance Backend:
- install the Data Governance Backend Helm chart:
  ```bash
	# Execute below commands from the helm_charts/data_gov_backend folder
	helm -n semantic-search install data-gov . &
  ```
- It takes a few minutes to start the app. In the pod's logs we should see after some time logs `Connection to Redis is ready` and `app started listening to requests`
# Using the app
- Access data governance UI using this URL in a browser: `localhost:8080`
- Log in using username `admin@admin.com` and password `admin`
- Using UI, create descriptions for tables which will be used for the semantic search and RAG system
# Architecture
## HTTP server and routes
We run API using ([[Backend Engineering - Running an API|link]]):
- Node.js as a HTTP server ([[Backend Engineering - API (HTTP, gRPC, etc.) server|link]]) (which receives requests and returns a response)
- Express to define routes / handlers ([[Backend Engineering - API endpoint, route and handler|link]]) (a logic for how to handle requests, generate a response)
## Databases and data models
Data that this backend uses:
- Database metadata about tables, columns and scripts
- Data lineage data

All this data is prepared by the metadata extraction pipeline - [[Data governance app with a RAG system - Metadata extraction pipeline|Metadata extraction pipeline]].

More information about it is here:
- [[Data governance app with a RAG system - Databases - Database documentation|Database documentation]] 
- [[Data governance app with a RAG system - Databases - Data lineage data|Data lineage data]] 
- [[Data governance app with a RAG system - Databases - Redis for caching|Redis for caching]] 
## Authentication and authorization
We use the Passport library and our own RBAC (with permissions stored in a database) for user authentication and authorization.

Available user roles:
- `newUser` - The default for every user. Can't see nor modify any data
- `viewer` - Can see all the data but can't modify it
- `designer` - Can see all the data and modify it

A new user can be created from the app, with the `newUser` role. To change this role, we need to set it up directly in the MongoDB database, the `userDocs` collection.

When starting the app, the admin user is created:
- username - admin@admin.com
- password - admin
- role - designer

The `modules/passport-config.js` script contains a function used for authenticating users.
## Caching - Redis
Redis is used for caching. More information is here - [[Data governance app with a RAG system - Databases - Redis for caching]].
# Features
## Data lineage visualizations
Data lineage visualizations are created using the `public/dataLineageScripts.js` script. It assigns x and y coordinates to nodes to position them properly on the screen.
## Authentication
- The `usersDocs` MongoDB collection is used 
## Semantic search
For semantic search we the `sortDocs` function which sorts table documents using semantic search (based on the semantic scores). 

It uses for that the Rest API route for semantic search ([[Data governance app with a RAG system - Semantic search API|link]]) which:
- takes a query as an input
- and provides a response with similarity scores between the given query and all the text chunks from all the documents.

The response in the following format:
```python
[
	{
		#ID of the table document (taken from the database documentation 
		# database)
		'object_id': object_id_1,
		# One text chunk from the document
		'text_chunk': text_chunk_1
		# Similarity score for this text chunk and the given query
		'similarity_score': similarity_score_1
	},
	...
]
```
## Creating descriptions for tables, columns, etc.
Using the UI, users can create descriptions for tables, columns, etc. They are saved in the database documentation database ([[Data governance app with a RAG system - Databases - Database documentation|link]]).
### Emitting a message to Kafka
When a table description gets updated, a message is emitted to Kafka ([[Data governance app with a RAG system - Kafka|link]]), to a specific topic, describing this event. 

This message is then processed by the embedding ingestion service ([[Data governance app with a RAG system - Embedding Ingestion Pipeline and Service|link]]) which clears a vector database and inserts there new embeddings for all the new, updated table descriptions.

For emitting messages we use a function defined in the `modules/kafka_producer.js` script which is used in the route for updating table descriptions, defined in the `routes/table_docs_route.js` script.
# Tooling
## Node.js
We use Node.js to run a HTTP server, more notes about it are here - [[Data governance app with a RAG system - Tools used - Node.js]].
### Running the app
- To run the app in the production mode:
> `node server.js` 
- To run the app in the dev mode (to allow us to modify app's code and see results without a need for restarting the app.):
> `npm run devStart`. 

Important info:
- The `devStart` command is specified in the `package.json` file. 
- When we set up the `NODE_ENV` env var to `development`, then running `npm install` will install all the packages from the `package.json` file including those under the `devDependencies` field.