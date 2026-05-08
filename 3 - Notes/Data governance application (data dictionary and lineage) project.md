Tags: [[_My_projects]] [[__Machine_Learning]]
#MyProjects #MachineLearning 

# Introduction
This is an application which:
- Enables creating a data dictionary (tables and columns descriptions)
- Search through a data dictionary using semantic search
- Automatically generates data lineage using SQL scripts from a SQL server and Sisense (a BI platform)
	- It shows how tables in a SQL server are being created 
	- And also which tables are used for which dashboards in Sisense

Technologies used:
- Express
- EJS
- MongoDB
- JavaScript, HTML, CSS
- Redis
# Code repository
Repository with the code for this project is here - [github.com](https://github.com/bulka4/ml_words_received_prediction).
# Data lineage 
## Data preparation
The `db_preparation/data_lineage_dashboards_docs.js` script prepares data which:
- Will be used for data lineage visualizations
- Is stored in MongoDB
- Is created automatically using SQL queries from the SQL server and Sisense

The `db_preparation/tables_docs.js` script prepares data in MongoDB about tables and columns for which we will be able to add descriptions in the application.
## Algorithm for creating a visualization
We create here a custom algorithm for creating data lineage visualizations.

That visualization consists of nodes connected by links and our algorithm calculates coordinates on the screen for each node such that they form a tree diagram.
# Model for semantic search
For semantic search we use a model from Hugging Face which we save in the onnx format. 

Before we run the application we save the model in the onnx format and saved onnx model is loaded by the application when it starts.

This is done by the `ml_model/model_preparation.py` script.
# EJS
We use EJS to create templated HTML files where we can insert values of variables.

So when user enters an endpoint, we can calculate values of variables and use them in the displayed HTML.

For example, when user enters some value into a field and clicks on a button, that button can:
- Redirect to a new endpoint
- Calculate values of variables using a value entered by a user
- Display HTML (a EJS file) with values of calculated variables
# User authentication
We use the Passport library for user authentication.
# Redis
Redis is used as in-memory database to make the web app working faster. Instead of loading data all the time from MongoDB (which is slow), we:
- Load data from MongoDB
- Saves it in Redis
- Next time user wants to load the data, it is loaded from Redis instead of MongoDB