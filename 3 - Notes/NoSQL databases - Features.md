Tags: [[_Databases]] [[_NoSQL_databases]]
#Databases #NoSQLDatabases 

# Introduction
They store documents (usually JSON-like). Each document is a collection of fields and different documents can contain different fields, for example:
```json
{"id": 1, "name": Alice, "age": 22}
{"id": 2, "name": Bob, "age": 25, "gender": male}
```

A document might not contain some field or it can contain that field with a null value, this is not the same:
```json
{"id": 1, "name": Alice, "age": 22}
{"id": 1, "name": Alice, "age": 22, "gender": null}
```