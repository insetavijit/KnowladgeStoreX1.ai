# Dependency Management & Conflicts

**Core definition:** The practice of resolving version clashes between libraries (e.g., Library A needs `numpy<2` and Library B needs `numpy>=2`).

**Position in ecosystem:**
The #1 reason Python environments break.

**Key idea:**
- **Lock Files:** Using `poetry.lock` or `requirements.txt` with specific hashes ensures everyone uses the *exact* same versions.
- **Pinning:** Explicitly stating `langgraph==0.1.5` prevents accidental upgrades that break your code.
- **Pip Check:** A command to scan for broken requirements.

## Troubleshooting Command

```bash
pip check
# Output: No broken requirements found.
```

If it says "X requires Y, which is not installed", you have a conflict.

## Quick Summaries

**30-second version:** It's like a seating chart at a wedding. You can't put Uncle Bob (Library A) next to Aunt Karen (Library B) or they will fight (crash). Dependency management is the careful planning that ensures everyone gets along.

**One-line recall:**
**Use lock files to freeze dependency versions and avoid runtime conflicts.**

---

## Linked Concepts
- [[Poetry vs pip Installation]]
- [[Virtual Environment Setup]]
- [[Upgrading LangGraph]]

---
**Last updated:** December 2025
