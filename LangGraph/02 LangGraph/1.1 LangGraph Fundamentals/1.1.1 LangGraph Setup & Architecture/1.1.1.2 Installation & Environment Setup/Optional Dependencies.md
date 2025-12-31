# Optional Dependencies

**Core definition:** Extra packages that enable specific advanced features in LangGraph, like **persistence** (Redis/Postgres) or **browser automation**.

**Position in ecosystem:**
Keep your install lightweight. Only install these if you actually use that specific feature.

**Key idea:**
- **Persistence:** `langgraph-checkpoint-sqlite` or `langgraph-checkpoint-postgres`.
- **Visualization:** `matplotlib` or `pygraphviz` (for drawing graph images).
- **Web Tools:** `playwright` (for browser-based agent tools).

## Common Extras

```bash
# For PostgreSQL Checkpointing
pip install langgraph-checkpoint-postgres

# For Graph Visualization
pip install grandalf
```

## Quick Summaries

**30-second version:** It's like downloading a video game. The base game works fine, but if you want the high-res textures (visualization) or multiplayer server (postgres persistence), you need to download the DLC packs.

**One-line recall:**
**Install extra packages only for specific features like DB persistence or plotting.**

---

## Linked Concepts
- [[Installing LangGraph]]
- [[Memory & Persistence]]
- [[Dependency Management & Conflicts]]

---
**Last updated:** December 2025
