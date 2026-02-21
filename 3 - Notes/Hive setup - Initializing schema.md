Tags: [[_Hive]] [[__Data_storage]] [[__Data_Engineering]]
#Hive #DataStorage #DataEngineering 

# Introduction
To use Hive Metastore, we need to initialize schema, that is to create all the necessary tables in the metadata db, using command:
```bash
schematool -dbType postgres -initSchema
```

where `-dbType` indicates what database we use, in this case it is PostgreSQL.