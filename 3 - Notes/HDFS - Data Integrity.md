Tags: [[__Data_Engineering]], [[__Distributed_computing]]

# Introduction
HDFS uses checksums to verify data integrity.

When data is written or read, HDFS validates it using these checksums.

Corrupt blocks are automatically detected and replaced from replicas.
# Checksums
A checksum is a short, fixed-size string of digits (often a hash) that uniquely represents the contents of a data block.
- It's generated using a hashing algorithm like CRC32, MD5, or SHA.

#DataEngineering #DistributedComputing 