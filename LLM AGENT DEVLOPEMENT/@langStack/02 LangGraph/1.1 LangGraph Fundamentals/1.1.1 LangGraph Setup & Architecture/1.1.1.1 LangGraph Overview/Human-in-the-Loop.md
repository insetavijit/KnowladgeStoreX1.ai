# Human-in-the-Loop

**Core definition:** **Human-in-the-Loop (HITL)** patterns allow execution to **pause** so a human can inspect the state, approve an action, or edit the data before the graph resumes.

**Position in ecosystem:**
Critical for high-stakes agents where you don't trust the AI to take final actions (like refunds or deleting files) automatically.

**Key idea:**
- **Interrupt:** Pause graph before a specific node (e.g., `interrupt_before=["action"]`).
- **Checkpoint:** Save state so it can be reloaded.
- **Resume:** Human sends a command to continue execution.

## Essential Characteristics

**1. Approval:** "Agent wants to send email. Allow? [Y/N]"
**2. Editing:** Human fixes a typo in the draft before sending.
**3. Time Travel:** Rewinding the graph to a previous step to try a different path.
**4. Debugging:** Pausing to inspect what went wrong in the middle of a run.

## Workflow

1.  Graph runs until it hits `action_node`.
2.  **PAUSE.** (Status: `interrupted`)
3.  System notifies user.
4.  User reviews state.
5.  User calls `graph.invoke(None, config)` to resume.

## Quick Summaries

**30-second version:** Like a learner driver with an instructor. The car (agent) drives itself, but the instructor (human) has a brake pedal. They can pause the car at an intersection, check if it's safe, and tell the driver to proceed or grab the steering wheel to correct them.

**One-line recall:**
**HITL allows humans to pause, review, and steer agent execution.**

---

## Linked Concepts
- [[Memory & Persistence]]
- [[Control Flow & Routing]]
- [[State Management]]

---
**Last updated:** December 2025
