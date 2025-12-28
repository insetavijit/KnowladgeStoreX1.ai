# What is an LLM Agent?

## Core Definition

An **LLM agent** is an autonomous system that embeds a large language model within a **control loop**, enabling iterative reasoning and action-taking to achieve explicit goals.

**Key difference from single LLM calls:**

- **Single call:** One prompt → one response (stateless)
- **Agent:** Continuous sense → think → act → observe cycle (stateful)

---

## Essential Characteristics

### **1. Multi-Step Execution**

Agents decompose complex objectives into sub-tasks and execute them sequentially or adaptively, rather than attempting everything in one shot.

### **2. Statefulness**

Agents maintain context across iterations through:

- Short-term memory (conversation history, scratchpad)
- Long-term memory (vector stores, episodic knowledge)

### **3. Explicit Goals**

Agents work toward defined objectives with termination conditions, unlike open-ended chat interactions.

### **4. Persistent Control Flow**

The agent maintains control and decides what to do next based on observations, creating a feedback loop: **perceive → reason → act → update → repeat**.

### **5. Tool Use**

Agents can invoke external actions (APIs, search, code execution, databases) and incorporate results into their decision-making.

---

## The Sense → Think → Act Loop

```
┌─────────────────────────────────────┐
│  SENSE: Perceive current state      │
│  ↓                                   │
│  THINK: Reason about next action    │
│  ↓                                   │
│  ACT: Execute tool/generate output  │
│  ↓                                   │
│  OBSERVE: Process results           │
│  ↓                                   │
│  UPDATE: Revise plan/memory         │
└─────────────────────────────────────┘
         ↓
    Repeat until goal achieved
```

This loop enables agents to:

- Adapt to unexpected results
- Correct mistakes through iteration
- Ground reasoning in real-world feedback
- Handle dynamic, unpredictable environments

---

## Core Components

|Component|Purpose|
|---|---|
|**LLM**|Reasoning engine for planning and decisions|
|**Tools**|External actions (APIs, search, code runners)|
|**Memory**|Context retention across iterations|
|**Controller**|Orchestrates the execution loop|
|**Guardrails**|Termination logic, safety checks, step limits|

---

## Architectural Spectrum: Workflows vs Agents

### **Agentic Workflows** (Structured)

- LLMs orchestrated through **predefined code paths**
- Predictable, deterministic
- Lower cost and latency
- **Use for:** Well-defined tasks (invoice processing, data extraction)

### **Autonomous Agents** (Flexible)

- LLMs **dynamically direct** their own processes
- Adaptive decision-making
- Higher cost, potential for errors
- **Use for:** Open-ended problems (research, complex coding)

**Principle:** Start simple. Use workflows for predictable tasks; reserve full agents for dynamic problems requiring model-driven decisions.

---

## Classic Pattern: ReAct (Reason + Act)

The foundational agent pattern interleaves reasoning with actions:

```
Thought: I need to find current weather data
Action: search("weather San Francisco today")
Observation: Temperature is 62°F, partly cloudy
Thought: I have the information needed
Action: Final Answer: It's 62°F and partly cloudy in San Francisco
```

**Why it works:** Grounds reasoning in real-world feedback, reduces hallucination, provides interpretability.

---

## When to Use Agents

✅ **Good fit:**

- Multi-step tasks where the path is unpredictable
- Workflows requiring external information or actions
- Dynamic environments needing adaptation
- Iterative problem-solving (debugging, research)

❌ **Poor fit:**

- Single-step or deterministic tasks
- Pure text transformations (summarization, translation)
- Latency-sensitive applications
- Cost-constrained environments

**Rule of thumb:** If you can write the steps in advance, use a workflow. If the LLM must decide what to do next, use an agent.

---

## Common Pitfalls & Fixes

|Pitfall|Mitigation|
|---|---|
|Hallucinated tool calls|Structured outputs, schema validation|
|Infinite loops|Max steps, progress tracking, stuck detection|
|Goal drift|Explicit objectives, periodic reflection|
|High cost/latency|Context compression, tiered models, caching|
|Compounding errors|Sandboxing, layered guardrails, validation|

---

## Quick Summaries

### **30-Second Version**

"An LLM agent wraps a language model in a control loop—sense, think, act, observe, repeat—so it can use tools, maintain memory, and work toward goals across multiple steps. Unlike a single LLM call that maps prompt to response, agents adapt based on feedback. They're ideal for complex, multi-step tasks like research or automation, but overkill for simple, predictable workflows."

### **One-Line Recall**

**LLM agent = LLM + tools + memory + control loop → autonomous, goal-directed, multi-step execution**

---

## Framework Options (2025)

- **LangGraph** — Stateful graphs with explicit control
- **AutoGen** — Multi-agent collaboration
- **CrewAI** — Role-based agent teams
- **Microsoft Agent Framework** — Unified SDK
- **Anthropic MCP** — Tool integration ecosystem

**Pro tip:** Start by using LLM APIs directly to understand the mechanics before adding framework complexity.

---

**Last Updated:** December 2025