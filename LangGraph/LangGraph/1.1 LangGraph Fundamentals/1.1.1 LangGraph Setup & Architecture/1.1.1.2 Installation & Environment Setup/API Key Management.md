# API Key Management

**Core definition:** Securely handling secrets like `OPENAI_API_KEY` so your agent can authenticate without leaking credentials in source code.

**Position in ecosystem:**
Security 101. If you push a key to GitHub, bots will steal it in seconds.

**Key idea:**
- **.env Files:** Store keys in a file named `.env` that is added to `.gitignore`.
- **libraries:** Use `python-dotenv` to load them.
- **Environment Variables:** LangGraph/LangChain automatically looks for specific env vars (e.g., `ANTHROPIC_API_KEY`).

## Setup Steps

1.  **Install:** `pip install python-dotenv`
2.  **Create `.env`:**
    ```env
    OPENAI_API_KEY=sk-proj-123456...
    TAVILY_API_KEY=tvly-abcdef...
    ```
3.  **Load in Python:**
    ```python
    from dotenv import load_dotenv
    load_dotenv() # Call this BEFORE importing langgraph logic
    ```

## Quick Summaries

**30-second version:** Never hardcode your password. Write it on a sticky note (the .env file) and tell your robot (the code) to read the note when it starts up. And make sure you don't accidentally glue that sticky note to the public bulletin board (GitHub).

**One-line recall:**
**Store keys in `.env`, ignore `.env` in git, and use `load_dotenv()`.**

---

## Linked Concepts
- [[Development Environment Setup]]
- [[Reference: API Key Management]] <!-- If generic note exists -->
- [[Troubleshooting Installation Issues]]

---
**Last updated:** December 2025
