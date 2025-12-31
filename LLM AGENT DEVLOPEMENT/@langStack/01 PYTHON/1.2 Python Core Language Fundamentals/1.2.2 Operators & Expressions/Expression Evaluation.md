**Core definition:** **Expression evaluation** is the runtime process by which Python executes a sequence of operations to produce a single value (object). It follows strict rules regarding evaluation order, operand resolution, and short-circuiting.

**Key idea:**

-   **Order:** strictly **Left-to-Right** (with precedence dictating grouping).
-   **Resolution:** Variables are resolved to objects immediately when evaluated.
-   **Side Effects:** Functions within expressions are executed as they are encountered.

## Why Expression Evaluation Matters

Understanding exact evaluation semantics prevents bugs in complex logic, especially when:

-   Functions have side effects (modifying global state, I/O).
-   Expressions rely on the state of previous parts of the same line.
-   Dealing with concurrency (understanding what operations are atomic).

## Core Evaluation Rules

**1. Left-to-Right Evaluation:**
Python evaluates expression arguments from left to right.
```python
foo() + bar()
```
`foo()` is guaranteed to execute before `bar()`. If `foo()` raises an exception, `bar()` is never called.

**2. Comparison Chaining:**
`a < b < c` evaluates `a`, then `b`. If `a < b` is true, it evaluates `c`. If false, `c` is **never evaluated**.

**3. Short-Circuiting:**
As discussed in Logical Operators, `and` and `or` stop evaluating as soon as the result is known.

**4. Argument Evaluation:**
In a function call `func(a(), b())`, `a()` runs first, then `b()`, then `func()` is called.

## Atomicity & Thread Safety (GIL Context)

In CPython (standard Python), expression evaluation is tied to the Global Interpreter Lock (GIL).

-   **Atomic:** Reading/replacing a single variable, appending to a list (`L.append(x)`).
-   **Not Atomic:** `i += 1`. This involves (1) read `i`, (2) add 1, (3) write `i`. A thread switch can occur between steps, leading to race conditions.

## Common Pitfalls

| Pitfall | Explanation |
| :--- | :--- |
| **Side Effects in Arguments** | If `a()` modifies a global that `b()` reads, `func(a(), b())` works. But `func(b(), a())` breaks it? No, arguments are eval'd left-to-right. So `func(b(), a())` runs `b` then `a`. Reliance on side-effect order makes code fragile. |
| **Default Mutable Arguments** | `def f(x=[]):` evaluates the default argument expression `[]` **once** at definition time, not at evaluation time. |
| **Generator Laziness** | Expressions inside a generator `(x for x in data)` are not evaluated until the generator is consumed (except for the outermost iterator). |

## Quick Summaries

**30-second version:**
Python evaluates expressions strictly from left to right. It resolves variables and executes function calls as it encounters them. Conditional operators (logic, comparisons) may skip parts of the expression (short-circuiting), which is critical for optimization and null-safety.

**One-line recall:**
**Evaluation = Left-to-right execution of the expression graph**

---

**Section:** **Expression Evaluation**
**Focus:** Understand how Python executes expressions
**Last updated:** December 2025

---
