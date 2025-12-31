# Virtual Environment Setup

**Core definition:** Creating an **isolated sandbox** for your project so that the libraries you install for LangGraph don't break your other projects (and vice versa).

**Position in ecosystem:**
Mandatory best practice. Python's global package namespace is fragile; "Dependency Hell" waits for those who skip this step.

**Key idea:**
- **Isolation:** Keeps `langgraph==0.1` here and `old-project-lib` there.
- **Tools:** `venv` (built-in), `conda`, or `virtualenv`.

## How to Set Up (Standard `venv`)

### 1. Create
```bash
# Windows
python -m venv .venv

# Mac/Linux
python3 -m venv .venv
```

### 2. Activate
```powershell
# Windows (PowerShell)
.\.venv\Scripts\Activate.ps1

# Mac/Linux
source .venv/bin/activate
```

### 3. Deactivate
```bash
deactivate
```

## Quick Summaries

**30-second version:** Imagine your computer is a kitchen. If you cook curry (Project A) and cake (Project B) in the same pot without washing it, everything tastes terrible. A virtual environment is like buying a brand new pot for every new recipe you try.

**One-line recall:**
**Always use a virtual environment to isolate project dependencies.**

---

## Linked Concepts
- [[Poetry vs pip Installation]]
- [[Python Version Requirements]]
- [[Dependency Management & Conflicts]]

---
**Last updated:** December 2025
