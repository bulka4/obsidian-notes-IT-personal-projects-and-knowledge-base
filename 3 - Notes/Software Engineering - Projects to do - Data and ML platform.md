Tags: [[_Obsidian]] [[_Software_Engineering]]
#Obsidian #SoftwareEngineering 

# Python SDK
[[Software Engineering - Projects to do - Data and ML platform - Python SDK]]
# Plugin architecture
Allow for creating plugins ([[Software Engineering - Plugins|link]]) so we can add new classes to be used without changing the application's code.

This demonstrates:
- dependency inversion
- interfaces
- factories
- extensibility
# Comprehensive testing
Not only
```
pytest
```

but
- unit and integration tests ([[Software Engineering - Testing|link]])
- end-to-end tests
- contract tests

Aim for
```
tests/ 
	unit/    
	integration/    
	e2e/
```
# CI pipeline
Instead of
```
pytest
```

have
```
lint
↓
type checking
↓
unit tests
↓
integration tests
↓
build Docker
↓
scan image
↓
deploy staging
↓
deploy production
```
# Observability
This is one of the biggest missing pieces.

Add
- metrics
- traces
- structured logs

using tools like OpenTelemetry, Prometheus, and Grafana.
# Documentation
Add architecture decision records (ADRs).

Explain
- Why Iceberg?
- Why Spark?
- Why Airflow?
- Why MLflow?
- Why not alternatives?

Senior engineers write these.