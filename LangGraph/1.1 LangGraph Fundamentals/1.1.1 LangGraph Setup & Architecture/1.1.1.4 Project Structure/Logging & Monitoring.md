# Logging & Monitoring

**Core Definition:** Setting up a centralized logging strategy so you can debug your agent in production without print statements.

**The Golden Rule:** **Use the `logging` module, not `print()`.**

## Centralized Logging Config

Create a `src/logger.py` to configure the format once.

```python
# src/logger.py
import logging
import sys

def setup_logger(name):
    logger = logging.getLogger(name)
    logger.setLevel(logging.INFO)
    
    handler = logging.StreamHandler(sys.stdout)
    formatter = logging.Formatter('%(asctime)s - %(name)s - %(levelname)s - %(message)s')
    handler.setFormatter(formatter)
    
    logger.addHandler(handler)
    return logger
```

## Usage in Nodes

```python
# src/nodes/search.py
from src.logger import setup_logger

logger = setup_logger(__name__)

def search_node(state):
    logger.info("Starting web search...")
    try:
        # ... logic ...
        logger.info("Search complete.")
    except Exception as e:
        logger.error(f"Search failed: {e}")
```

## LangSmith Tracing

Logging captures *text lines*, but LangSmith captures *structures*.
-   Ensure `LANGCHAIN_TRACING_V2=true` is in your `.env`.
-   Your logs tell you "The search started."
-   LangSmith tells you "The search returned these 5 documents."

## Quick Summary

**1-Line Recall:** **Configure Python `logging` centrally and use it in every node; combine with LangSmith for full observability.**
