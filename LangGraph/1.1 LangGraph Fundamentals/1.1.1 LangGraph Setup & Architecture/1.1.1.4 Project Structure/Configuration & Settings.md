# Configuration & Settings

**Core Definition:** Managing variables that change between environments (Local, Staging, Prod) or runs (Model names, API keys).

**The Golden Rule:** **Never hardcode configuration.**

## 1. Environment Variables (`.env`)
Secrets (API Keys) and infrastructure settings (Database URL) belong here.
-   Use `python-dotenv` to load them.
-   Use `pydantic-settings` to validate them.

```python
# src/config.py
from pydantic_settings import BaseSettings

class Settings(BaseSettings):
    openai_api_key: str
    tavily_api_key: str
    model_name: str = "gpt-4o"
    
    class Config:
        env_file = ".env"

settings = Settings()
```

## 2. Runtime Configuration (`configurable`)
LangGraph allows passing config *at runtime* (per request). This is useful for:
-   Letting the user choose the model.
-   Setting a specific `system_prompt` version.
-   Passing a `user_id`.

```python
# Accessing runtime config in a node
def my_node(state, config):
    user_model = config.get("configurable", {}).get("model", "gpt-3.5")
    ...
```

## 3. Prompts as Config
Don't bury prompts in code.
-   Store them in `src/prompts.py` OR
-   Pull them from LangChain Hub.

## Quick Summary

**1-Line Recall:** **Use Pydantic Settings for environment variables and LangGraph's `config` dictionary for per-run dynamic settings.**
