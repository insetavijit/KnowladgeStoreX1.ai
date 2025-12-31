**Core definition:** **Operator precedence** determines the order in which operations are parsed and evaluated in an expression containing multiple operators. It is the set of rules that tells Python which "math problem" to solve first.

**Key idea:**

-   **Hierarchy:** Higher precedence operators bind more tightly (are evaluated first).
-   **Associativity:** Determines order for operators with the same precedence (usually left-to-right).
-   **Override:** Parentheses `()` always override default precedence.

## Why Operator Precedence Matters

Without precedence rules, expressions would be ambiguous. Does `3 + 4 * 5` mean `(3+4)*5 = 35` or `3+(4*5) = 23`? Python uses standard mathematical conventions (PEMDAS) extended to cover programming concepts like logic and bitwise operations to ensure deterministic evaluation.

## The Precedence Hierarchy (Highest to Lowest)

| Rank | Operator | Description | Associativity |
| :--- | :--- | :--- | :--- |
| 1 | `(expression)` | Parentheses | - |
| 2 | `f(args)`, `x[i]`, `x.attr` | Function call, subscription, slicing, attribute | Left-to-right |
| 3 | `**` | Exponentiation | **Right-to-left** |
| 4 | `~`, `+x`, `-x` | Bitwise NOT, Unary plus/minus | - |
| 5 | `*`, `/`, `//`, `%` | Multiplication, Division, Remainder | Left-to-right |
| 6 | `+`, `-` | Addition, Subtraction | Left-to-right |
| 7 | `<<`, `>>` | Bitwise shifts | Left-to-right |
| 8 | `&` | Bitwise AND | Left-to-right |
| 9 | `^` | Bitwise XOR | Left-to-right |
| 10 | `\|` | Bitwise OR | Left-to-right |
| 11 | `==`, `!=`, `<`, `<=`, `>`, `>=` | Comparisons, Identity, Membership | Chained |
| 12 | `not` | Logical NOT | - |
| 13 | `and` | Logical AND | Left-to-right |
| 14 | `or` | Logical OR | Left-to-right |
| 15 | `if - else` | Conditional Expression (Ternary) | Left-to-right |
| 16 | `:=` | Assignment Expression (Walrus) | - |

## Execution Semantics & Associativity

**1. Left-to-Right Associativity (Standard):**
Most operators bind from left to right.
`10 - 4 - 3` is calculated as `(10 - 4) - 3 = 3`.

**2. Right-to-Left Associativity (Exponentiation):**
The `**` operator binds from right to left.
`2 ** 3 ** 2` is calculated as `2 ** (3 ** 2)` -> `2 ** 9 = 512`.
*(Note: Be careful! `(2 ** 3) ** 2` would be `64`)*.

## Common Pitfalls

| Pitfall | Explanation |
| :--- | :--- |
| **Bitwise vs Comparison** | `x & 1 == 0` evaluates as `x & (1 == 0)` because `==` is lower distinct than `&`? **NO!** Actually `==` is *lower* priority than `&`, so it parses as `(x & 1) == 0`. Wait... let's check the table. `&` is rank 8, `==` is rank 11. Lower number = higher priority? **Correction:** The table above ranks 1 as highest. So `&` (8) executes *before* `==` (11). Correct. Pitfall: `not x == y` parses as `not (x == y)`. |
| **Chained Comparisons** | `a < b < c` is **not** `(a < b) < c`. It is `(a < b) and (b < c)`. |
| **Boolean Logic Mix-ups** | `x or y and z` parses as `x or (y and z)` because `and` binds tighter than `or`. |

> [!TIP]
> **When in doubt, use parentheses.**
> It is better to write `(a + b) * c` explicitly than to rely on memory of the precedence table. Explicit is better than implicit.

## Quick Summaries

**30-second version:**
Python evaluates expressions based on a strict hierarchy. Arithmetic `* /` beats `+ -`. Bitwise `&` beats `|`. Comparison beats operators. Logical `not` beats `and`, which beats `or`. Exponentiation `**` is unique as it groups from right-to-left.

**One-line recall:**
**Precedence = The default order of operations (BEDMAS/PEMDAS on steroids)**

---

**Section:** **Operator Precedence**
**Focus:** Determine evaluation order in expressions
**Last updated:** December 2025

---
