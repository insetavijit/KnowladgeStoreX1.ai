**Core definition:** **Logical operators** in Python (`and`, `or`, `not`) interpret operands in a boolean context and return a result based on truthiness. They are essential for combining conditions and implementing control flow logic.

**Key idea:**

-   **Operands:** Boolean expressions or any object (evaluated for truthiness).
-   **Operators:** `and`, `or`, `not`.
-   **Result:** `True`, `False`, or one of the operands (due to short-circuiting).

## Why Logical Operators Matter

Logical operators are the glue that combines simple checks into complex decision trees. They allow:

-   Validating multiple requirements simultaneously
-   Providing default values (fallback logic)
-   Building complex guard clauses
-   Negating conditions for readability

## Core Logical Operators

| Operator | Name | Behavior |
| :--- | :--- | :--- |
| `and` | Logical AND | Returns true if **both** operands are true. |
| `or` | Logical OR | Returns true if **at least one** operand is true. |
| `not` | Logical NOT | Inverts the boolean value of the operand. |

## Execution Semantics & Short-Circuiting

Python’s logical operators are **short-circuit operators**. They evaluate operands from left to right and stop as soon as the result is determined. This is a crucial performance and safety feature.

**1. `and` Behavior:**
-   Evaluates left operand.
-   If **False**, returns the left operand immediately (does not evaluate right).
-   If **True**, evaluates and returns the right operand.

**2. `or` Behavior:**
-   Evaluates left operand.
-   If **True**, returns the left operand immediately (does not evaluate right).
-   If **False**, evaluates and returns the right operand.

**3. Return Values:**
Unlike comparison operators that always return `bool`, logical operators return **the last evaluated object**.
-   `"apple" and "banana"` returns `"banana"` (truthy).
-   `None or "default"` returns `"default"`.

## Example Evaluation Flow

```python
result = True or (1 / 0)  # Safe!
           ↓
    Left is True -> Stop.
    Return True.
    (Division by zero never happens)
```

## Common Pitfalls

| Pitfall | Explanation |
| :--- | :--- |
| **Bitwise Confusion** | Using `&` / `|` instead of `and` / `or`. Bitwise operators do not short-circuit and work on bits. |
| **Precedence Errors** | `not` has higher precedence than `and`, which is higher than `or`. |
| **"Is NOT" vs "Not Is"** | `x is not y` is an identity check; `not x is y` negates the identity check result. |
| **Truthy Chaining** | `a == b or c` checks if `a==b` OR `c` is truthy, not if `a` equals `b` or `c`. Correct: `a in (b, c)`. |

## Relationship to Python’s Type System

Logical operators rely on the `__bool__` (or `__len__`) dunder method of objects to determine "truthiness".
-   **Falsy values:** `False`, `None`, `0`, `0.0`, `""`, `[]`, `{}`, `()`.
-   **Truthy values:** Everything else.

## Quick Summaries

**30-second version:**
Logical operators (`and`, `or`, `not`) combine boolean expressions. Crucially, `and` and `or` define control flow via short-circuiting: they return the determining operand rather than a strict boolean, which allows for patterns like default value assignment (`name = input or "Guest"`).

**One-line recall:**
**Logical operators = Short-circuiting combiners of truth**

---

**Section:** **Logical Operators**
**Focus:** Combine or negate boolean expressions
**Last updated:** December 2025

---
