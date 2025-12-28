# Version Compatibility

**Core Definition:** Managing the dependency relationship between **LangGraph** (the orchestrator) and **LangChain** (the component library).

**The Challenge:** The AI ecosystem moves fast. Breaking changes happen. Understanding how packages relate saves you from "ImportError hell."

## The Package Split

LangChain is no longer one giant monorepo. It is split:

1.  **`langchain-core`**: The base interfaces (Runnable, Message, BaseChatModel).
    -   *LangGraph relies heavily on this.*
2.  **`langchain`**: The chains, agents, and retrieval logic.
3.  **`langchain-community`**: Third-party integrations.
4.  **`langgraph`**: The separate orchestration library.

## Best Practices

### 1. Pin Dependencies
Always pin your `requirements.txt` or `pyproject.toml`.
```text
langchain-core==0.2.10
langgraph==0.1.5
langchain-openai==0.1.7
```

### 2. Watch `langchain-core`
Since LangGraph uses `langchain-core` objects (like `AIMessage`) as its state currency, a breaking change in `core` affects LangGraph.
-   Fortunately, `core` is designed to be very stable now (post v0.1).

### 3. Pydantic v1 vs v2
This was a major pain point in 2023/2024.
-   Modern LangChain/LangGraph is fully **Pydantic v2** native.
-   Ensure you aren't mixing v1 and v2 libraries if possible.

## Upgrading
When you upgrade LangGraph, check if it requires a newer `langchain-core`.
-   `pip install -U langgraph langchain-core` (Update them together).

## Quick Summary

**1-Line Recall:** **LangGraph depends chiefly on `langchain-core`; keep these two packages updated in sync to avoid compatibility issues.**
