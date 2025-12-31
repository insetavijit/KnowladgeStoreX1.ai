# Installing LangGraph

**Core definition:** The action of downloading the `langgraph` library from PyPI and installing it into your environment.

**Position in ecosystem:**
Step 0. You can't build agents without the library.

**Key idea:**
- **Package Name:** `langgraph` (Note: NOT `langchain`-graph or similar).
- **Source:** PyPI (Python Package Index).
- **Command:** `pip install langgraph`.

## The Command

```bash
# Basic install
pip install langgraph

# With specific extras (if any available/needed)
pip install langgraph[all]
```

## Verifying Install
Always verify that it actually installed:

```bash
python -c "import langgraph; print(langgraph.__version__)"
```

## Common Issues
- **Permission Denied:** Don't use `sudo`! Use a [[Virtual Environment Setup]].
- **SSLCertVerification:** Corporate firewall issues.
- **Name Conflict:** Don't name your own file `langgraph.py`!

## Quick Summaries

**30-second version:** It's a one-line command. Just make sure you are in your virtual environment first, or you'll install it globally and clutter your system settings.

**One-line recall:**
**`pip install langgraph` gets you the core framework.**

---

## Linked Concepts
- [[LangChain Dependency Installation]]
- [[Optional Dependencies]]
- [[Validating the Setup]]

---
**Last updated:** December 2025
