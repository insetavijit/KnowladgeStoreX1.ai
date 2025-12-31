# Poetry vs pip Installation

**Core definition:** A comparison of **Package Managers**. **pip** is the default installer. **Poetry** (and **uv**) are advanced tools for dependency resolution and packaging.

**Position in ecosystem:**
For quick scripts, `pip` is fine. For production agents, `Poetry` or `uv` prevents "it works on my machine" syndrome.

**Key idea:**
- **pip:** Simple, manual. Requires `requirements.txt`.
- **Poetry:** Robust. Uses `pyproject.toml` and `poetry.lock` to guarantee exact versions.
- **uv:** The new fast kid on the block (from Astral), compatible with pip APIs but much faster.

## Comparison Table

| Feature | pip | Poetry | uv |
| :--- | :--- | :--- | :--- |
| **Speed** | Medium | Slow | Extreme |
| **Lock File** | No (manual) | Yes (Auto) | Yes |
| **VirtualEnv** | Manual | Auto-managed | Choice |
| **Resolution** | Basic | Strict | Strict |

## Commands

**pip:**
```bash
pip install langgraph
pip freeze > requirements.txt
```

**Poetry:**
```bash
poetry add langgraph
```

## Quick Summaries

**30-second version:** Pip is like buying groceries without a list; you might forget what brand of milk you bought last time. Poetry is like a strict inventory system that records the exact barcode of every item you buy, so your friend can cook the exact same meal.

**One-line recall:**
**Use pip for speed; use Poetry/uv for stability and reproducibility.**

---

## Linked Concepts
- [[Installing LangGraph]]
- [[Virtual Environment Setup]]
- [[Dependency Management & Conflicts]]

---
**Last updated:** December 2025
