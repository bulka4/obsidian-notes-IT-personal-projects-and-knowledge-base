Tags: [[__Data_Engineering]] [[_Data_architecture]]
#DataEngineering #DataArchitecture  

# Introduction
Mater data is data related to entities, i.e. objects like:
- Customer
- Product
- Employee

Master data is a data which is:
- Cleaned and transformed
- standardized, deduplicated, and governed
- Combined from all the sources
- Considered as a source of truth

We might have for example two systems with data about customers and master data combines and unifies data from both of them.
# Low-level vs high-level master data
Low-level master data usually means master data that is closer to detailed operational entities, as opposed to higher-level, aggregated business entities.

The meaning depends on context, but common examples:
## Product hierarchy example
High-level master data:
```
Product Category
    └── Electronics
```

Lower-level master data:
```
Product
    └── Laptop Dell XPS 15
        └── SKU: DELL-XPS-15-2026-001
```

The SKU/product record is lower-level because it represents a specific entity.