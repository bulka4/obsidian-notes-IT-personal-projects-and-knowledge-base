Tags: [[_Spark]]
#Spark 

# Introduction
Spark session is an execution context created when a client connects to a SQL engine. It is a process which can take a SQL statement and execute it.

Inside a session, Spark:
- loads catalog ([[Data storage catalog|link]]) metadata
- caches information
- remembers configuration
- keeps runtime statistics
- keeps temporary objects
- keeps internal optimizer behavior settings
	- That creates execution plans which determines how SQL statements are executed

