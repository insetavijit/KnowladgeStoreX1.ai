# Data & Fixtures

**Core Definition:** Organizing the static data needed to run or test your agent.

**The Problem:** Hardcoding "example inputs" or "prompt few-shot examples" directly into Python files makes them hard to read and edit.

## The `data/` Directory

Create a top-level `data/` folder.

```text
data/
├── prompts/           # Text files for large prompts
│   ├── system.md
│   └── few_shot.json
├── fixtures/          # Mock data for testing
│   ├── mock_search_results.json
│   └── sample_state.json
└── examples/          # Runnable examples for users
    └── quickstart.py
```

## Using Fixtures in Tests

In `pytest`, loading data from a file is cleaner than defining big dicts.

```python
# tests/conftest.py
import json
import pytest

@pytest.fixture
def sample_state():
    with open("data/fixtures/sample_state.json") as f:
        return json.load(f)
```

## Versioning Data

If your agent relies on a specific CSV or slightly large file (~5MB), it's okay to commit it to Git.
-   **Warning:** If it's >50MB, use **Git LFS** or just document where to download it (S3/GCS).

## Quick Summary

**1-Line Recall:** **Keep large strings, JSON blobs, and CSVs out of your code; put them in a dedicated `data/` directory.**
