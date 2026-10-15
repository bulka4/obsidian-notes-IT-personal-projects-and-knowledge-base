Tags: [[_Python]] [[__Programming_languages]]
#Python #ProgrammingLanguages 

# Introduction
With the Python `logging` module we can collect logs like this:
```python
import logging

logger = logging.getLogger(__name__)

logger.info("Embedding ingestion started")

try:
    ingest_embeddings()

except Exception:
    logger.exception("Embedding ingestion failed")
    raise
```

They can be sent to different places:
- `stdout / stderr`
- files