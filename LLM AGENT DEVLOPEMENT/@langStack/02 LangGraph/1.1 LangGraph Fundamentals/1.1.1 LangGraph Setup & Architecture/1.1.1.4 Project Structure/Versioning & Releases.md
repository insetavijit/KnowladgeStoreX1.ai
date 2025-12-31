# Versioning & Releases

**Core Definition:** Communicating changes to your users and maintaining history.

**The Problem:** "I changed the prompt and now the agent is broken."

## Semantic Versioning (SemVer)
Apply SemVer to your agent logic.
-   **Major (1.0.0):** Breaking change to the Graph Structure (e.g., removed a node).
-   **Minor (1.1.0):** Added a new Tool or Node (backward compatible).
-   **Patch (1.0.1):** Prompt tweaks or bug fixes.

## Tracking Versions in Code

It is useful to return the version in the agent's metadata.

```python
# src/__init__.py
__version__ = "0.1.0"
```

```python
# In your API
@app.get("/info")
def info():
    return {"version": __version__}
```

## Changelog
Keep a `CHANGELOG.md`. Agents evolve fast.
-   "2023-10-12: Switched from OpenAI to Anthropic for the 'Reasoning' node."
-   "2023-10-15: Added 'Retry' edge to the Search code."

## Quick Summary

**1-Line Recall:** **Version your agent like software; a prompt change is a code change.**
