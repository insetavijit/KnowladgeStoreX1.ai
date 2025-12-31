# src Directory Convention

**Core Definition:** The practice of putting all application source code inside a root `src/` directory, rather than at the top level of the project.

**Why Use It?**
1.  **Isolation:** Keeps code separate from config files (`pyproject.toml`, `.env`, `Dockerfile`).
2.  **Import Hygiene:** Forces you to install your package (even locally) to run it, preventing "it works on my machine" import errors.
3.  **Clarity:** Anyone opening the repo knows exactly where the logic lives.

## Standard Structure for LangGraph

```text
my-agent/
├── pyproject.toml
├── .env
├── src/
│   ├── my_agent/          # Namespace package
│   │   ├── __init__.py
│   │   ├── graph.py       # Graph definition
│   │   ├── state.py       # State definitions
│   │   ├── nodes/         # Node logic
│   │   │   ├── __init__.py
│   │   │   ├── agent.py
│   │   │   └── tools.py
│   │   └── utils/
└── tests/
```

## Python Packaging

With `src/`, you typically install your project in "editable mode" during development:
`pip install -e .`

This allows you to do absolute imports anywhere:
`from my_agent.nodes.agent import agent_node`

## Quick Summary

**1-Line Recall:** **Using a `src/` directory prevents import confusion and keeps the project root clean for configuration files.**
