Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
We can scan container images for vulnerabilities.

Example:
```
Docker image:

Ubuntu
 ├── vulnerable OpenSSL
 ├── old Python package
 └── application code
```

A scanner checks for:
- known CVEs
- outdated packages
- malware

Tools:
- Trivy
- Clair
- Snyk