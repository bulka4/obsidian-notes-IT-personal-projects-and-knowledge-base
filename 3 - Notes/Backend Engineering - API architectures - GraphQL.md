Tags: [[_Software_Engineering]]
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
A resolver function is a JavaScript function that fetch data, for example:
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
