Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
JSON Schema is a schema definition format for JSON data. It describes the structure, types, and validation rules of JSON documents.

Example JSON:
```JSON
{
  "id": 123,
  "name": "Alice"
}
```

JSON Schema:
```JSON
{
  "type": "object",
  "properties": {
    "id": {
      "type": "integer"
    },
    "name": {
      "type": "string"
    }
  }
}
```

It defines:
- which fields exist
- data types
- required/optional fields
- validation rules
# Why to use it
JSON Schema is used to validate the structure of JSON data. The workflow is like this:
- we read a JSON data
- using JSON schema we validate this data (check whether it contains all the fields with correct types)
- Through an error if validation fails (there are some missing or unexpected fields, data types are incorrect)