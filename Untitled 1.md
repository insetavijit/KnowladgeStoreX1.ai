# What is an LLM Agent?

**Core definition:** An **LLM agent** is an autonomous system that places a large language model inside a **control loop** so it can repeatedly think and act to reach clear goals.

**Key difference:**

- **Single call:** One prompt → one response (stateless)
    
- **Agent:** Continuous **sense → think → act → observe** cycle (stateful)
    

## Essential Characteristics

**1. Multi-step execution:** Breaks complex goals into smaller tasks and solves them step by step or as needed.  
**2. Statefulness:** Keeps context using short-term memory (history, notes) and long-term memory (vector stores, past experiences).  
**3. Explicit goals:** Works toward defined goals with clear stopping conditions.  
**4. Persistent control flow:** Keeps a feedback loop: **perceive → reason → act → update → repeat**.  
**5. Tool use:** Calls APIs, search, code execution, databases, and uses the results.

## Sense → Think → Act Loop

```
SENSE → THINK → ACT → OBSERVE → UPDATE → repeat until goal achieved
```

Helps the agent adjust to surprises, fix mistakes over time, base reasoning on real results, and work in changing environments.

## Core Components

|LLM|Tools|Memory|Controller|Guardrails|
|---|---|---|---|---|
|Thinking & planning engine|External actions|Keeps context|Runs the loop|Safety, limits, stopping rules|

## Workflows vs Agents

**Agentic workflows (structured):** Fixed code paths; predictable, reliable, lower cost and faster.  
_Use for:_ clear tasks (invoice processing, data extraction).

**Autonomous agents (flexible):** Let the model choose the next steps; more adaptive but higher cost and risk of errors.  
_Use for:_ open-ended problems (research, complex coding).

**Principle:** Start with workflows; use agents when the model must decide what to do next.

## Classic Pattern: ReAct (Reason + Act)

```
Thought → Action → Observation → Thought → Final Answer
```

_Why it works:_ Ties thinking to real feedback, lowers hallucinations, and makes reasoning easier to follow.

## When to Use Agents

**Good fit:**

- Multi-step, unpredictable paths
    
- Need external info or actions
    
- Changing environments
    
- Step-by-step problem-solving (debugging, research)
    

**Poor fit:**

- Single-step or fixed tasks
    
- Simple text changes
    
- Apps that need very low delay
    
- Tight cost limits
    

**Rule:** If steps are known → workflow. If the model must choose → agent.

## Common Pitfalls & Fixes

|Pitfall|Mitigation|
|---|---|
|Made-up tool calls|Structured outputs, schema checks|
|Infinite loops|Max steps, progress tracking, stuck detection|
|Drifting goals|Clear objectives, reflection|
|High cost/latency|Shorter context, cheaper models, caching|
|Errors building up|Sandboxing, guardrails, validation|

## Quick Summaries

**30-second version:** An LLM agent wraps a model in a sense–think–act loop so it can use tools, keep memory, and work toward goals over many steps. It learns from feedback—great for complex tasks, too much for simple ones.

**One-line recall:**  
**LLM agent = LLM + tools + memory + control loop → autonomous, goal-driven, multi-step execution**

## Framework Options (2025)

**LangGraph** (stateful graphs), **AutoGen** (multi-agent), **CrewAI** (role teams), **Microsoft Agent Framework** (SDK), **Anthropic MCP** (tool ecosystem).  
_Pro tip:_ Start with basic LLM APIs before adding framework complexity.

---

**Last updated:** December 2025

---