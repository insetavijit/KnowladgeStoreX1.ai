# LangChain Dependency Installation

**Core definition:** How **LangGraph** relates to and pulls in **LangChain**.

**Position in ecosystem:**
LangGraph is built *on top* of LangChain. You often need both: LangGraph for the flow, and LangChain for the specific prompts, models, and tools.

**Key idea:**
- **Peer Dependency:** LangGraph installs `langchain-core` automatically.
- **Full Install:** You typically want `langchain` (main package) or `langchain-community` for non-standard tools.

## Installation Command

```bash
# Recommended standard stack
pip install langgraph langchain langchain-openai
```

## Why do I need them?
- **LangGraph:** Managing the loop/state.
- **LangChain Core:** The `Runnable` and `Message` primitives.
- **LangChain OpenAI:** The actual LLM connection.

## Quick Summaries

**30-second version:** You wouldn't buy a car engine (LangGraph) without wheels (models) or a chassis (LangChain Core). While LangGraph technically handles the "logic," you need the other LangChain packages to actually do useful work like calling GPT-4 or searching Google.

**One-line recall:**
**LangGraph controls the flow; LangChain provides the bricks.**

---

## Linked Concepts
- [[Installing LangGraph]]
- [[Optional Dependencies]]
- [[Role in Agent Stack]]

---
**Last updated:** December 2025
