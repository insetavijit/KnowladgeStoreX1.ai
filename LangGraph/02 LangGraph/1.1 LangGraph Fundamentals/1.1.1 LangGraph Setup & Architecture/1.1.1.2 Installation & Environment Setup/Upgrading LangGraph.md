# Upgrading LangGraph

**Core definition:** The process of moving to a newer version of the library to get bug fixes or new features.

**Position in ecosystem:**
LangGraph is evolving fast (Beta -> Stable). Frequent updates are common.

**Key idea:**
- **Semantic Versioning:** Watch out for MAJOR changes (0.x to 1.x).
- **Release Notes:** Always read them before running the upgrade command.
- **The Command:**

```bash
# Upgrade just langgraph
pip install --upgrade langgraph

# Upgrade everything in requirements.txt
pip install --upgrade -r requirements.txt
```

## Safety Checklist
1.  Check [GitHub Releases](https://github.com/langchain-ai/langgraph/releases) page.
2.  Run tests *immediately* after upgrading.
3.  If broken, downgrade: `pip install langgraph==0.1.0`.

## Quick Summaries

**30-second version:** Software ages like milk, not wine. You need to keep it fresh. But sometimes the new milk tastes different. Always taste-test (run unit tests) immediately after buying a new carton.

**One-line recall:**
**`pip install --upgrade langgraph`, but read release notes first.**

---

## Linked Concepts
- [[Installing LangGraph]]
- [[Dependency Management & Conflicts]]
- [[Testing Environment]]

---
**Last updated:** December 2025
