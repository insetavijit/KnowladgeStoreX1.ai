# Stateful vs Stateless Nodes

**Core Definition:**
-   **Stateless Node:** Only relies on the `state` argument passed to it. Pure.
-   **Stateful Node:** Relies on external variables, global scope, or persistent connections (like a DB connection pool).

## The Goal: Be Stateless
LangGraph nodes should ideally be **Pure Functions**:
`f(state) -> update`

## Handling External State (Connections)
You don't want to open a new DB connection every time a node runs.

### 1. Global Resources (The easy way)
Initialize the connection at module level.
```python
# Global scope
db = Database()

def query_node(state):
    return db.query(...)
```
*Risk: Hard to test, hard to reset.*

### 2. Dependency Injection via `config` (The robust way)
Pass resources via the `configurable` dict or a bound context.

```python
# Definition
def query_node(state, config):
    db = config["configurable"]["db_connection"]
    ...
```

## Why it Matters
If nodes are stateless, you can:
-   Parallelize them easily.
-   Move them to different machines (mostly).
-   Test them without setting up a complex environment.

## Quick Summary

**1-Line Recall:** **Strive for Stateless nodes; if you need database connections, inject them via configuration rather than using globals.**
