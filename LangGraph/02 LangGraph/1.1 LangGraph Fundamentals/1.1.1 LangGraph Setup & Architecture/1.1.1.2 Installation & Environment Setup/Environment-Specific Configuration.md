# Environment-Specific Configuration

**Core definition:** Changing how the app behaves based on where it's running (e.g., using a local SQLite DB in development, but a cloud Postgres DB in production).

**Position in ecosystem:**
Hardcoding configuration is a deadly sin.

**Key idea:**
- **ENV Variables:** Use `APP_ENV=development` or `APP_ENV=production`.
- **Conditional Logic:** Code that reads the var and swaps components.

## Code Example

```python
import os
from langgraph.checkpoint.sqlite import SqliteSaver
from langgraph.checkpoint.postgres import PostgresSaver

app_env = os.getenv("APP_ENV", "development")

if app_env == "production":
    checkpointer = PostgresSaver.from_conn_string(os.getenv("DB_URL"))
else:
    # Use simple local file for dev
    checkpointer = SqliteSaver.from_conn_string(":memory:")
```

## Quick Summaries

**30-second version:** You wear sweatpants at home (Dev) and a suit to the office (Prod). Your agent should do the same: use lightweight tools when you're building it, and heavy-duty, robust tools when it's working for real customers.

**One-line recall:**
**Use environment variables to switch between Dev (SQLite) and Prod (Postgres) configs.**

---

## Linked Concepts
- [[API Key Management]]
- [[Docker & Containerization]]
- [[Memory & Persistence]] <!-- From 1.1.1.1 -->

---
**Last updated:** December 2025
