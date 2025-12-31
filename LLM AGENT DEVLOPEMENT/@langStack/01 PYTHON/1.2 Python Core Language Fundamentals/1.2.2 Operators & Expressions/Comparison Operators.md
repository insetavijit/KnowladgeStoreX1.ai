**Core definition:** **Comparison operators** (also known as relational operators) in Python are symbols that evaluate the relationship between two operands, always producing a **Boolean value** (`True` or `False`) based on the comparison logic.

**Key idea:**

-   **Operands:** Any Python objects (numbers, strings, lists, etc.)
-   **Operators:** Symbols such as `==`, `!=`, `<`, `>`, `<=`, `>=`
-   **Result:** A `bool` indicating if the relation holds true.

## Why Comparison Operators Matter

Comparison operators are the decision-making engines of a program. They allow code to:

-   Execute branching logic (`if`, `while`)
-   Filter datasets and query databases
-   Sort collections based on value
-   Validate state and inputs

## Core Comparison Operators

| Operator | Name | Behavior |
| :--- | :--- | :--- |
| `==` | Equal to | Returns `True` if values are equal |
| `!=` | Not equal to | Returns `True` if values are different |
| `>` | Greater than | Returns `True` if left > right |
| `<` | Less than | Returns `True` if left < right |
| `>=` | Greater than or equal | Returns `True` if left >= right |
| `<=` | Less than or equal | Returns `True` if left <= right |

> [!NOTE]
> **Identity Operators (`is`, `is not`)** are distinct from comparison operators. `==` checks **value equality** (do they look the same?), while `is` checks **object identity** (are they the same atom in memory?).

## Execution Semantics

**1. Chained Comparisons:**
Python supports mathematical chaining of comparisons, which is syntactic sugar for `and` operations.
`10 < x < 20` is evaluated as `(10 < x) and (x < 20)`, but `x` is only evaluated once.

**2. Type Compatibility:**
-   **Numeric Types:** You can compare `int` and `float` safely (`5 == 5.0` is `True`).
-   **Incompatible Types:** Comparing ordered types (like `str` and `int`) with `<`, `>` raises a `TypeError`. Equality checks (`==`, `!=`) between incompatible types are valid and simply return `False`.

**3. Short-Circuiting:**
In chained comparisons, evaluation stops as soon as one condition returns `False`.

## Example Evaluation Flow

```python
x = 15
result = 10 < x < 20
         ↓
    (10 < 15) and (15 < 20)
       ↓            ↓
      True   and   True
             ↓
           True
```

## Common Pitfalls

| Pitfall | Explanation |
| :--- | :--- |
| **Float Equality** | `0.1 + 0.2 == 0.3` is `False` due to precision limits. Use `math.isclose()`. |
| **Confusing `is` and `==`** | `is` is for singletons (`None`) or identity checks; `==` is for values. |
| **String sorting** | Strings compare lexicographically (ASCII value), so `"Z" < "a"`. |
| **None comparisons** | Never use `== None`; always use `is None`. |

## Relationship to Python’s Type System

Comparison behavior is defined by **Magic Methods** (Dunder methods) in the class definition:

-   `==` maps to `__eq__(self, other)`
-   `!=` maps to `__ne__(self, other)`
-   `<` maps to `__lt__(self, other)`
-   `>` maps to `__gt__(self, other)`
-   `<=` maps to `__le__(self, other)`
-   `>=` maps to `__ge__(self, other)`

If a class does not implement ordering methods (`__lt__`, etc.), attempting to sort instances will raise a `TypeError`.

## Quick Summaries

**30-second version:**
Comparison operators evaluate the relationship between two values and return a Boolean. They support mathematical chaining (`a < b < c`) and rely on object-level implementations (`__eq__`, `__lt__`). While they handle numeric type conversion automatically, comparing disparate types for order raises errors.

**One-line recall:**
**Comparison operators = Relational questions → Boolean answers**

---

**Section:** **Comparison Operators**
**Focus:** Compare values and produce boolean results
**Last updated:** December 2025

---
