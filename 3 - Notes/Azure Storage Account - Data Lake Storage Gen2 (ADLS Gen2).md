Tags: [[__Data_storage]] [[_Azure_Storage_Account]]
#DataStorage #AzureStorageAccount 

# Introduction
ADLS Gen2 is built on top of Blob Storage ([[Azure Storage Account - Blob Storage|link]]) but it adds file-system semantics:
- Hierarchical namespace - There are directories containing files
- Atomic renaming and moving files - When renaming or moving files, the operation is either completely successful or doesn't make any impact. We can't end up with a partially performed operation.
- POSIX-like ACLs ([[POSIX-like ACL|link]])
- ABFS driver is used to connect to it