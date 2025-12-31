# Environment Files & Secrets

**Core Definition:** Safety protocols for handling sensitive data (API Keys, Passwords).

**The Golden Rule:** **GIT IGNORE YOUR SECRETS.**

## 1. The `.env` Pattern
-   **`.env`**: The actual file with secrets. **ADD TO .gitignore**.
-   **`.env.example`**: The template file with blank values. **COMMIT THIS**.

```text
# .env.example
OPENAI_API_KEY=sk-placeholder
TAVILY_API_KEY=tvly-placeholder
LANGCHAIN_TRACING_V2=true
```

## 2. Using `python-dotenv`
Load the `.env` file at the very entry point of your app.

```python
# src/main.py
from dotenv import load_dotenv

load_dotenv() # Finds .env automatically
```

## 3. Secret Managers (Production)
In production (AWS/GCP), don't use `.env` files. Inject secrets as environment variables into the container.
-   Your code using `os.environ` or `pydantic-settings` will work exactly the same way in both Dev (.env) and Prod (Env Vars).

## Quick Summary

**1-Line Recall:** **Commit `.env.example`, ignore `.env`; never paste an API key directly into Python code.**
