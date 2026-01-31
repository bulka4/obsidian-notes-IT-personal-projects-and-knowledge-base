Tags: [[__Data_Engineering]] [[_Airflow]]
#DataEngineering #Airflow 

# Introduction
An Airflow connection is a named, centrally managed set of credentials and configuration that operators and Airflow internals use to talk to external systems.

Thanks to connections, we don't need to hardcode credentials in code.

Credentials are stored in Airflow metadata database.
# Connection anatomy
Every connection has:
- ID - Unique name (a string)
- Type - Azure Blob, S3, Postgres etc.
- Login
- Password
- Extra - JSON for advanced config
# Creating a connection
A connection can be created using:
## Airflow UI
Navigate to Admin > Connections and click on + (add a new connection).
## CLI
```bash
airflow connections add "azure_blob" \
    --conn-type "wasb" \
    --conn-login "<client_id>" \
    --conn-password "<client_secret>" \
    --conn-extra '{"tenant_id": "<tenant_id>", "account_name": "<storage_account_name>"}'
```
## Environment variables
```bash
export AIRFLOW_CONN_<connection_name>='wasb://<container>@<account>.blob.core.windows.net?tenant_id=<tenant_id>&client_id=<client_id>&client_secret=<client_secret>'
```
## Helm
```yaml
extraConnections:
  - id: azure_blob
    type: wasb
    login: <client_id>
    password: <client_secret>
    extra: '{"tenant_id": "<tenant_id>", "account_name": "<storage_account_name>"}'
```