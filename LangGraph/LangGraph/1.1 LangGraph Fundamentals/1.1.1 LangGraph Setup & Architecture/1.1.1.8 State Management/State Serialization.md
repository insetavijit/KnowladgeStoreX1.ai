# State Serialization

**Core Definition:** Converting the in-memory Python State object into JSON (or bytes) for storage.

## Why Serialization is Hard
Your state might contain:
-   `AIMessage` objects.
-   Pydantic models.
-   Custom classes.

## Serde (Serialization/Deserialization)
LangGraph handles standard types automatically.
-   **Messages:** Converted to dicts `{"type": "ai", "content": "..."}`.
-   **Primitives:** Kept as is.

## Custom Objects
If you start putting complex, non-serializable objects (like a `socket` or `thread.lock`) in your state:
1.  Checkpointing will FAIL.
2.  You cannot persist the graph.

## Best Practice
**Only store JSON-serializable data in State.**
If you need a database connection, do NOT put it in State. Put it in the global verify or pass it via `configurable` config.

## Quick Summary

**1-Line Recall:** **Keep State JSON-serializable to ensure checkpointing works; convert complex objects to dictionary representations before storing.**
