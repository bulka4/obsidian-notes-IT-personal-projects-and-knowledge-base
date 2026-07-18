Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
Do not put secrets inside images:

Bad:
```
ENV PASSWORD=my_password
```

because secrets become part of the image/history.

Better:
```
Container
    |
    ↓
Secret manager
    |
    ↓
Database password
```

Examples:
- Kubernetes Secrets
- HashiCorp Vault
- Cloud secret managers (Azure Key Vault, AWS Secrets Manager)