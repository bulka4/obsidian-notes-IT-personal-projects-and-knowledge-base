Tags: [[_Python]] [[__Programming_languages]] [[_Software_Engineering]]
#Python #ProgrammingLanguages #SoftwareEngineering 

# Introduction
In Python, we can use the `logging` module for saving logs. 
# Usage
```python
import logging

logging.basicConfig(level=logging.INFO)

logging.info("Starting application")
logging.warning("Low disk space")
logging.error("Database connection failed")
```
# Severity levels
It supports different severity levels:

| Level      | Purpose                               |
| ---------- | ------------------------------------- |
| `DEBUG`    | Detailed information for debugging    |
| `INFO`     | Normal application events             |
| `WARNING`  | Something unexpected but not critical |
| `ERROR`    | A failure occurred                    |
| `CRITICAL` | Serious failure, application may stop |

A severity level is included together with a log message.
# Output
Using this logging module we can:
- Print messages in a console
- Save logs in a file
- Sent logs to a centralized logging system
- Trigger notifications
# Features
Logging systems usually allow us to:
- Send logs to monitoring systems, save them in files
- Add timestamps and metadata
- Filter messages by severity