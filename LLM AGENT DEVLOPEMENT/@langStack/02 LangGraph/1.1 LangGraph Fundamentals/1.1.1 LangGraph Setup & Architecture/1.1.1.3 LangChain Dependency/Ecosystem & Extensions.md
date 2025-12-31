# Ecosystem & Extensions

**Core Definition:** The suite of tools surrounding LangGraph that help with deployment, debugging, and sharing. LangGraph isn't an island; it's part of a platform.

## 1. LangSmith (Observability)
**The Debugger.**
-   **Role:** Tracing, Testing, and Monitoring.
-   **Vital for Graphs:** It renders the graph structure visually and lets you click into each node to see inputs/outputs.
-   **Dataset Testing:** You can run your graph against 100 examples in LangSmith to check accuracy before deploying.

## 2. LangServe (Deployment)
**The API Layer.**
-   **Role:** Turn your graph into a production REST API with one line of code.
-   **Magic:** It automatically creates endpoints for `/invoke`, `/stream`, and `/batch`.
-   **Graph Integration:** It supports `astream_events`, allowing your frontend to see exactly which node is running in real-time.

```python
# serve.py
add_routes(app, graph, path="/agent")
```

## 3. LangChain Hub
**The Registry.**
-   **Role:** Share and discover prompts and agents.
-   **Usage:** You can download a "Reference RAG Agent" from the hub to get a starter graph structure.

## 4. LangGraph Studio
**The IDE.**
-   A dedicated desktop/web environment specifically for developing LangGraph agents.
-   It visualizes the graph dynamically as you code and lets you interact with it (chat) while inspecting the state.

## Quick Summary

**1-Line Recall:** **LangSmith helps you debug it; LangServe helps you deploy it; LangGraph Studio helps you build it.**
