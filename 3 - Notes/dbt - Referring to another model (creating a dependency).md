Tags: [[_dbt]] [[__Data_Engineering]]
#dbt #DataEngineering 

# Introduction
In dbt we can use `ref('model_name')` to refer to another dbt model and create a dependency between those models.

For example, if we have models like this:
```bash
|-- models
	|-- model_1.sql
	|-- model_2.sql
```

`model_1.sql`:
```sql
select 1 as col
```

`model_2.sql`:
```sql
select * from {{ ref('model_1') }}
```

then `{{ ref('model_1.sql') }}` refers to the `model_1.sql` model and that creates a dependency (model 2 will not be built until the model 1 has been built).

In the `ref()` we need to provide name of the file from the `models` folder, without the `.sql` extension.