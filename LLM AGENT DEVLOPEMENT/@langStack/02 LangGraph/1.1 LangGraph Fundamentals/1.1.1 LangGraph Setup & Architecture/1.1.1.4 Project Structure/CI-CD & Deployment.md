# CI-CD & Deployment

**Core Definition:** Automating the testing and shipping of your agent.

**Why?** Agents are fragile. An upgrade to OpenAI's model or a prompt change can break them. You need automated guards.

## Recommended CI Workflow (GitHub Actions)

1.  **Code Quality:** Run `ruff` or `black` (Linting).
2.  **Unit Tests:** Run `pytest tests/unit` (Fast).
3.  **Integration:** Run `pytest tests/integration` (Slow, requires API keys).
    -   *Note: You need to add `OPENAI_API_KEY` to your GitHub Repo Secrets.*

## Dockerizing LangGraph

Since LangGraph is just Python, it Dockerizes easily.

```dockerfile
# Dockerfile
FROM python:3.11-slim
WORKDIR /app
COPY . .
RUN pip install -e .
CMD ["python", "src/main.py"]
```

## Deployment Options

1.  **LangGraph Cloud:** The optimized, managed platform.
2.  **FastAPI / LangServe:** Self-hosted API container.
    -   Docker container runs `uvicorn src.server:app`.

## Quick Summary

**1-Line Recall:** **Automate linting and testing in CI; package your agent as a standard Docker container for deployment.**
