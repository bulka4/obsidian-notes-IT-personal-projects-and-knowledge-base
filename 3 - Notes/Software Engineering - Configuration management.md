Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
**Configuration management** is the process of managing and controlling application settings that determine how software behaves in different environments.

Instead of hardcoding values:
```python
database_url = "localhost:5432"
```

configuration is stored separately:
```
Application
    |
    ↓
Configuration
    |
    ├── database URL
    ├── API keys
    ├── feature flags
    └── environment settings
```

Examples of configuration:
- database connection strings
- API endpoints
- authentication settings
- logging levels
- feature flags
- resource limits
# Why it is needed
Without configuration management:
- changing environments requires code changes
- secrets can leak into source code
- deployments become harder

Example:
```
Development:
DB_HOST=localhost

Production:
DB_HOST=prod-db.company.com
```

The same code runs with different configurations.
# Common techniques
## Environment variables
```python
import os

db_host = os.getenv("DB_HOST")
```
## Configuration files
Example:
```
database:
  host: localhost
  port: 5432

logging:
  level: INFO
```
## Configuration management tools
Examples:
- Kubernetes ConfigMaps and Secrets
- HashiCorp Vault (secrets)
- AWS Parameter Store
- Azure App Configuration