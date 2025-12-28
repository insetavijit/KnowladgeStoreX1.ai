# Testing Environment

**Core definition:** The tools and configuration needed to **validate** your graphs automatically, including unit tests (pytest) and integration tests.

**Position in ecosystem:**
Graphs are logic pipelines. You must test that branching logic works before deploying to production.

**Key idea:**
- **Framework:** `pytest` is the standard.
- **Async Support:** `pytest-asyncio` is required because LangGraph is async-native.
- **Mocking:** You need to mock the LLM calls so testing doesn't cost money.

## Basic Setup

```bash
pip install pytest pytest-asyncio
```

## Example Test File

```python
import pytest
from my_graph import workflow

@pytest.mark.asyncio
async def test_simple_path():
    app = workflow.compile()
    result = await app.ainvoke({"messages": ["hello"]})
    assert "response" in result
```

## Quick Summaries

**30-second version:** You wouldn't drive a car that hasn't been crash-tested. Testing environments let you "crash" your agent in a safe simulator (your laptop) to ensure it handles errors correctly before you let real users talk to it.

**One-line recall:**
**Use `pytest` and `pytest-asyncio` to validate graph logic.**

---

## Linked Concepts
- [[Development Environment Setup]]
- [[Testing & Debugging]] <!-- From 1.1.1.1 -->
- [[Validating the Setup]]

---
**Last updated:** December 2025
