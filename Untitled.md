# What is an LLM Agent?

**Core definition:** An **LLM agent** is an autonomous system that embeds a large language model within a **control loop** to iteratively reason and act toward explicit goals.

**Key difference:**

- **Single call:** One prompt → one response (stateless)
    
- **Agent:** Continuous **sense → think → act → observe** cycle (stateful)
    

## Essential Characteristics

**1. Multi-step execution:** Decomposes complex objectives into sub-tasks, executed sequentially or adaptively.  
**2. Statefulness:** Maintains context via short-term memory (history, scratchpad) and long-term memory (vector stores, episodic knowledge).  
**3. Explicit goals:** Operates toward defined objectives with termination conditions.  
**4. Persistent control flow:** Maintains feedback loop: **perceive → reason → act → update → repeat**.  
**5. Tool use:** Invokes APIs, search, code execution, databases, and integrates results.

## Sense → Think → Act Loop

```
SENSE → THINK → ACT → OBSERVE → UPDATE → repeat until goal achieved
```

Enables adaptation to unexpected results, iterative correction, grounded reasoning, and handling dynamic environments.

## Core Components

|LLM|Tools|Memory|Controller|Guardrails|
|---|---|---|---|---|
|Reasoning & planning|External actions|Context retention|Orchestrates loop|Safety, limits, termination|

## Workflows vs Agents

**Agentic workflows (structured):** Predefined code paths; predictable, deterministic, lower cost/latency.  
_Use for:_ well-defined tasks (invoice processing, data extraction).

**Autonomous agents (flexible):** Dynamically direct processes; adaptive but higher cost/error risk.  
_Use for:_ open-ended problems (research, complex coding).

**Principle:** Start with workflows; use agents when the model must decide what to do next.

## Classic Pattern: ReAct (Reason + Act)

```
Thought → Action → Observation → Thought → Final Answer
```

_Why it works:_ Grounds reasoning in feedback, reduces hallucinations, improves interpretability.

## When to Use Agents

**Good fit:**

- Multi-step, unpredictable paths
    
- External info/actions required
    
- Dynamic environments
    
- Iterative problem-solving (debugging, research)
    

**Poor fit:**

- Single-step/deterministic tasks
    
- Pure text transforms
    
- Latency-sensitive apps
    
- Cost-constrained setups
    

**Rule:** If steps are known → workflow. If the model must choose → agent.

## Common Pitfalls & Fixes

|Pitfall|Mitigation|
|---|---|
|Hallucinated tools|Structured outputs, schema validation|
|Infinite loops|Max steps, progress tracking, stuck detection|
|Goal drift|Explicit objectives, reflection|
|High cost/latency|Context compression, tiered models, caching|
|Compounding errors|Sandboxing, guardrails, validation|

## Quick Summaries

**30-second version:** An LLM agent wraps a model in a sense–think–act loop so it can use tools, keep memory, and pursue goals across steps. It adapts via feedback—ideal for complex tasks, overkill for simple workflows.

**One-line recall:**  
**LLM agent = LLM + tools + memory + control loop → autonomous, goal-directed, multi-step execution**

## Framework Options (2025)

**LangGraph** (stateful graphs), **AutoGen** (multi-agent), **CrewAI** (role teams), **Microsoft Agent Framework** (SDK), **Anthropic MCP** (tool ecosystem).  
_Pro tip:_ Start with raw LLM APIs before adding framework complexity.

---

**Last updated:** December 2025

---
