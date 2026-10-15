Tags: [[__Software_Engineering]]
#SoftwareEngineering 

# Introduction
GraphQL is an API query language which allows us to get data by making a query like this:
```
{
  user(id: 1) {
    name
    orders {
      id
      total
    }
  }
}
```

This query is:
- Sent over HTTP
- Parsed by a GraphQL engine
- Each field is “resolved” - For each field, GraphQL calls a resolver function.
# Resolver functions
A resolver function is a function that fetch data, for example:
```javaScript
User: {
  name: (user) => user.name,
  orders: (user) => getOrdersByUserId(user.id)
}
```

It can fetch data from any database.
# Schema
We need to have defined schema where we define data types, for example:
```
type User {
  id: ID
  name: String
  orders: [Order]
}

type Order {
  id: ID
  total: Float
}
```
# Comparison to the REST GET method
Using REST API and the GET method we can get exactly the same behavior as using GraphQL:
- We take parameters from the URL for the GET method
- We process them using our function and return a result

but we need to implement on our own all the features that GraphQL already provides (described in the section below). 
# Features
GraphQL provides a standardized way for:
- Field selection - Client can include in the request only specific fields, doesn't have to include all of them in every request
- Nested queries - Client requests related data, e.g. a user and their orders
- Query parsing - Parses GraphQL query syntax into a structured representation
- Schema validation - Checks requested fields, arguments and types against the schema