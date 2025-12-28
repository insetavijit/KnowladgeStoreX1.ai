# Testing Directory Structure

**Core Definition:** Mirroring your source code structure inside the `tests/` directory to facilitate unit and integration testing.

**Why?** If you change `src/nodes/agent.py`, you should know exactly where to look for the corresponding tests (`tests/nodes/test_agent.py`).

## Recommended Structure

```text
tests/
├── conftest.py          # Global fixtures (mock LLMs, test state)
├── integration/         # End-to-end graph runs
│   └── test_graph.py
└── unit/                # Individual component tests
    ├── nodes/
    │   ├── test_agent.py
    │   └── test_tools.py
    └── tools/
        └── test_search.py
```

## Key Components

### 1. `conftest.py`
Place your standard mocks here.
```python
@pytest.fixture
def mock_state():
    return {"messages": [], "user_id": "test"}
```

### 2. Unit Tests
Test nodes in isolation. Invoke the node function directly with a mock state dictionary. You don't need to compile the graph to test one node.

### 3. Integration Tests
Test the compiled graph (`workflow.compile()`).
-   Use `langchain-core.tracers.context` to capture runs.
-   Check that executing Node A actually leads to Node B.

## Quick Summary

**1-Line Recall:** **Mirror your `src` structure in `tests/unit` and keep slow end-to-end tests in `tests/integration`.**
