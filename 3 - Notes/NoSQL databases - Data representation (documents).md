Tags: [[_Databases]]
#Databases  

# Introduction
NoSQL databases store documents (usually JSON-like). Documents are grouped into collections.

Each document consist of fields and different documents can contain different fields, for example:
```json
{"id": 1, "name": Alice, "age": 22}
{"id": 2, "name": Bob, "age": 25, "gender": male}
```

So a collection of documents is similar to a table, where documents are rows, but not all the documents from the same collection need to contain the same fields and saying that a document doesn't contain a field is not the same as saying that it contains that field but with a null value.
# Field with null vs no field
A document might not contain some field or it can contain that field with a null value, this is not the same:
```json
{"id": 1, "name": Alice, "age": 22}
{"id": 1, "name": Alice, "age": 22, "gender": null}
```

When we select a field from a specific document and that field doesn't exist, the result we get is an empty document:
```json
{}
```
while if we try to select a field which does exist and its value is null, the result is a document with null as that field's value:
```json
{"gender": null}
```
