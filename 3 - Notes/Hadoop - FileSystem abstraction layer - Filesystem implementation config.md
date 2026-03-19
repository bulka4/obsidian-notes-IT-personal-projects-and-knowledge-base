Tags: [[_Hadoop]] 
#Hadoop 

# Introduction
When we want Hadoop's FileSystem layer ([[Hadoop - FileSystem abstraction layer|link]]) to use some specific filesystem scheme, we need to tell it how to handle it in the `core-site.xml` file.

For example if we want to use `abfss` (Azure ADLS Gen2), then we need to set up:
```xml
<property>
  <name>fs.abfss.impl</name>
  <value>org.apache.hadoop.fs.azurebfs.SecureAzureBlobFileSystem</value>
</property>

<property>
  <name>fs.abfs.impl</name>
  <value>org.apache.hadoop.fs.azurebfs.AzureBlobFileSystem</value>
</property>
```

These properties tell Hadoop:
- When the URI scheme is `abfss://` → use `SecureAzureBlobFileSystem`
- When the URI scheme is `abfs://` → use `AzureBlobFileSystem`

If this config is missing (or the required `hadoop-azure` jars are not on the classpath), Hadoop cannot resolve the scheme and you may get an error like:
```bash
No FileSystem for scheme "abfss"
```