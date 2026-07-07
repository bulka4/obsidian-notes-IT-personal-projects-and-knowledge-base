Tags: [[_Obsidian]] [[_Software_Engineering]]

# Backend refactor
Split
```
controllers
services
repositories
models
api
workers
```

instead of everything together.
# Async workers
Move lineage generation into background jobs.
```
Queue
↓
Worker
↓
Database
↓
Notification
```
# Versioning
Track
```
Lineage v1
↓
Lineage v2
↓
Diff
```
# REST API
Instead of only UI.
# Search API
Allow
```
GET /tables
GET /lineage
GET /columns
```
# Pagination
- Sorting
- Filtering
- Caching
