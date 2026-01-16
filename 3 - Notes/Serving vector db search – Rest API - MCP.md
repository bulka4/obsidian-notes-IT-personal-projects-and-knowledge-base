Tags: [[_Vector_databases]]
#VectorDatabases

# Introduction
We can prepare a vector db, which stores data on disk, and create a long running service which enables other apps to search through this db.

We can create for example a Rest API or MCP server to which other apps can send a question and it will send similar docs from a vector db as a response.

We can create this Rest API on our own or use a vector db which provides such an API, for example Chroma.
### Example
Here is an example script of creating our own Rest API where we use FAISS as a vector db which stores data in memory. It consists of two parts.

In the first part we:
- Convert docs into vector embeddings
- Save embeddings in a vector db
- Save vector db in a file
![[2 - Images/AI agents/Screenshot 3.png]]

In the second part we:
- Load the vector db from a file
- Create a Rest API where we find docs similar to a question

Finding similar docs is done in the following way:
- Convert a question into a vector embedding
- Find similar vectors in a vector db
![[2 - Images/AI agents/Screenshot 4.png]]

There are also tools for building vector dbs which provides Rest APIs and which can store data on a disk.