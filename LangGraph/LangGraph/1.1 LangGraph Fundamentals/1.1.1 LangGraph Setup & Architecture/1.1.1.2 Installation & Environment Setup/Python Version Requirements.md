# Python Version Requirements

**Core definition:** The specific version constraints of the Python interpreter required to run LangGraph efficiently and without syntax errors.

**Position in ecosystem:**
LangGraph is a modern library that leverages recent Python features (like type hinting improvements), so it doesn't support ancient Python versions.

**Key idea:**
- **Minimum:** Python 3.9+ (due to `typing` module usage).
- **Recommended:** Python 3.11+ (significant speed improvements).
- **Incompatible:** Python 2.x, Python 3.8 and older.

## Why 3.9+?
LangGraph relies heavily on:
1.  **Type Hints:** `list[int]` vs `List[int]` (introduced in 3.9).
2.  **Asyncio:** Performance improvements in newer kernels.
3.  **Pydantic v2:** Core dependency which favors newer Python.

## Checking Your Version

```bash
python --version
# Output: Python 3.11.4
```

## Quick Summaries

**30-second version:** Don't try to run this on that old Windows 7 laptop with Python 3.6. Update to the latest stable Python (3.11 or 3.12) to get free speed boosts and avoid weird "SyntaxError" bugs related to type annotations.

**One-line recall:**
**LangGraph requires Python 3.9 or higher; 3.11 is recommended.**

---

## Linked Concepts
- [[Virtual Environment Setup]]
- [[Installing LangGraph]]
- [[Troubleshooting Installation Issues]]

---
**Last updated:** December 2025
