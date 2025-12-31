**Core definition:** The **Walrus Operator** (`:=`), officially known as the **Assignment Expression**, allows you to assign a value to a variable *inside* an expression. It returns the value being assigned, enabling "calculate and use" patterns in a single step. introduced in Python 3.8.

**Key idea:**

-   **Syntax:** `NAME := EXPRESSION`
-   **Behavior:** Evaluates the expression, assigns it to `NAME`, and **returns** the result.
-   **Purpose:** Reduces code duplication and improves readability in specific patterns (loops, conditionals).

## Why the Walrus Operator Matters

Before Python 3.8, assignment was a statement, not an expression. You could not assign `x = 5` inside an `if` statement. The walrus operator bridges this gap, allowing dense, efficient code structures by removing the need to initialize variables *before* a check.

## Core Use Cases

**1. While Loops (The Killer Feature):**
Reading data until a condition is met (e.g., file reading, regex, sockets).

*Without Walrus:*
```python
chunk = file.read(1024)
while chunk:
    process(chunk)
    chunk = file.read(1024)  # Duplicated code!
```

*With Walrus:*
```python
while (chunk := file.read(1024)):
    process(chunk)
```

**2. List Comprehensions (Filter and Map):**
Calculating a value, checking it, and then using it, all in one pass.

*Without Walrus:*
```python
results = []
for x in data:
    y = f(x)
    if y > 10:
        results.append(y)
```

*With Walrus:*
```python
# Calculates f(x) once, checks > 10, retains value
results = [y for x in data if (y := f(x)) > 10]
```

**3. Regex Matches:**
Checking for a match and using the match object immediately.

```python
if (match := pattern.search(line)):
    print(match.group(1))
```

## Execution Semantics & Comparison

| Feature | Assignment Statement (`=`) | Assignment Expression (`:=`) |
| :--- | :--- | :--- |
| **Context** | Standalone line | Inside `if`, `while`, lists, etc. |
| **Returns Value** | No | **Yes** (returns the assigned value) |
| **Precedence** | Not applicable (statement) | Lowest (often requires parens) |

## Common Pitfalls

| Pitfall | Explanation |
| :--- | :--- |
| **Readability** | Overusing `:=` in complex lines creates "write-only" code. Use it only when it *simplifies* flow. |
| **Scope Bleeding** | Variables defined by `:=` in a list comprehension **leak** into the surrounding scope (function scope), unlike normal loop variables. |
| **Precedence** | `:=` has the **lowest** precedence. `if x := True or False` parses as `x := (True or False)`. `if x := 5 > 3` parses as `x := (5 > 3)` -> `x = True`. |
| **Unnecessary Use** | `x := 5` on its own line is legal but unidiomatic. Use `x = 5`. |

## Quick Summaries

**30-second version:**
The Walrus Operator (`:=`) assigns a value to a variable and returns that value simultaneously. It is best used in `while` loops and list comprehensions to avoid recalculating functions or duplicating method calls. It was added in Python 3.8 to streamline "loop-and-a-half" patterns.

**One-line recall:**
**Walrus Operator = Assign + Return (in one bite)**

---

**Section:** **Walrus Operator**
**Focus:** Assign values within expressions to reduce duplication
**Last updated:** December 2025

---
