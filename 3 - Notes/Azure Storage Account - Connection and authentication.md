Tags: [[__Data_storage]] [[_Azure_Storage_Account]]
#DataStorage #AzureStorageAccount 

# URL scheme
We can use two URL schemes:
- `wasbs://` - Used for connecting to a Blob Storage and ADLS Gen2
- `abfss://` - Used for connecting to ADLS Gen2

They are used in a URL we use for connecting:
```
wasbs://{containerName}@{storageAccount}.blob.core.windows.net
```

For each scheme we use different driver / SDK to connect and different authentication methods are supported.
# Driver / SDK used
Depending on which scheme we will use, different drivers / SDKs will be used for connecting and authentication:
- `wasbs://` uses `BlobServiceClient` SDK
- `abfss://` uses `DataLakeServiceClient` SDK

# Authentication method
`wasbs` scheme which uses `BlobServiceClient` SDK, supports authentication through a connection string (we can create a `AZURE_STORAGE_CONNECTION_STRING` env var with a connection string which uses access key).

`abfss` scheme which uses `DataLakeServiceClient` SDK, uses Azure AD (service principal, managed identity, or interactive login) for authentication.
# wasbs authentication
To authenticate when connecting using the `wasbs` URL scheme, we can use the `AZURE_STORAGE_CONNECTION_STRING` env var of the following format:
```bash
DefaultEndpointsProtocol=https;AccountName=${STORAGE_ACCOUNT_NAME};AccountKey=${STORAGE_ACCOUNT_ACCESS_KEY};EndpointSuffix=core.windows.net
```
where access key is base64 encoded.