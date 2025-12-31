# Troubleshooting Installation Issues

**Core definition:** A guide to fixing common errors when `pip install langgraph` fails or when the library won't import.

**Position in ecosystem:**
Environments are messy. Things break.

**Key idea:**
- **ImportError:** Usually a circular import or naming conflict (did you name your script `langgraph.py`?).
- **ModuleNotFoundError:** You are likely in the wrong virtual env.
- **SSL Error:** Corporate firewall/VPN blocking PyPI.

## Top 3 Fixes

1.  **"No module named langgraph":**
    *   Check `which python` or `Get-Command python`. Is it in `.venv`?
2.  **"Circular Import":**
    *   Rename your file from `langgraph.py` to `main.py`.
3.  **"Dependency Conflict":**
    *   Nuke it from orbit: `rm -rf .venv` and start over.

## Quick Summaries

**30-second version:** 90% of installation issues are because you think you are in the virtual environment, but you aren't. Close your terminal, open it again, activate the venv, and try again.

**One-line recall:**
**Verify your active environment and file naming before panicking.**

---

## Linked Concepts
- [[Validating the Setup]]
- [[Virtual Environment Setup]]
- [[Dependency Management & Conflicts]]

---
**Last updated:** December 2025
