# Tool & Integration Modules

**Core Definition:** Separating external capabilities (Tools) and API wrappers (Integrations) from the core agent logic.

**Why?** Tools often require messy imports, API clients, and pydantic models. You don't want this cluttering your node logic.

## Recommended Structure

```text
src/
├── tools/
│   ├── __init__.py      # Exposes list of tools
│   ├── search.py        # Tavily/Google wrapper
│   ├── calculator.py    # Math logic
│   └── database.py      # SQL tools
```

## Best Practices

### 1. The `TOOLS` Constant
It's helpful to export a list of all available tools from the package.

```python
# src/tools/__init__.py
from .search import web_search
from .calculator import add, multiply

ALL_TOOLS = [web_search, add, multiply]
```

### 2. Wrapping Third-Party Libraries
Don't use raw API clients inside nodes. Wrap them.
-   *Bad:* Calling `stripe.Charge.create(...)` inside `node_payment`.
-   *Good:* Creating a `StripeTool` that handles errors and formatting, then calling that tool.

### 3. Testing Tools
Isolate tools so you can test them without running the whole agent.
`pytest tests/tools/test_calculator.py`

## Quick Summary

**1-Line Recall:** **Tools are the messy interface to the outside world; hide that mess in a `src/tools` module so your agent logic stays pure.**
