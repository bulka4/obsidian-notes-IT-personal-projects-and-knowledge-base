Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
Idempotency means that performing the same operation multiple times has the same final effect as performing it once.

For example, a HTTP request can be idempotent when performing the same request multiple times ends up with the same result as if performed once.

It is important to make sure we don't end up with duplicated when failures occur and we perform retries.