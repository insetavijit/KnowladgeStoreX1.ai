**Core definition:** **Bitwise operators** perform operations directly on the binary representations (bits) of integers. They allow for low-level data manipulation, masking, and efficient mathematical shifts.

**Key idea:**

-   **Operands:** Integers (treated as sequences of bits).
-   **Operators:** `&` (AND), `|` (OR), `^` (XOR), `~` (NOT), `<<` (Left Shift), `>>` (Right Shift).
-   **Result:** A new integer resulting from the bit-level transformation.

## Why Bitwise Operators Matter

While less common in high-level business logic, bitwise operators are critical for:

-   **Optimization:** Storing multiple boolean flags in a single integer (bitmasks).
-   **Systems Programming:** Interfacing with hardware or binary file formats.
-   **Math Tricks:** Fast multiplication/division by powers of 2 (shifts).
-   **Cryptography & Hashing:** Manipulating data blocks efficiently.

## Core Bitwise Operators

| Operator | Name | Behavior | Example (`a=5` mixed `0101`, `b=3` mixed `0011`) |
| :--- | :--- | :--- | :--- |
| `&` | Bitwise AND | Sets bit to 1 if **both** bits are 1. | `5 & 3` → `1` (`0101 & 0011 = 0001`) |
| `\|` | Bitwise OR | Sets bit to 1 if **at least one** bit is 1. | `5 \| 3` → `7` (`0101 \| 0011 = 0111`) |
| `^` | Bitwise XOR | Sets bit to 1 if bits are **different**. | `5 ^ 3` → `6` (`0101 ^ 0011 = 0110`) |
| `~` | Bitwise NOT | Inverts all bits (flips 0 to 1 and 1 to 0). | `~5` → `-6` (Two's complement result) |
| `<<` | Left Shift | Shifts bits left, filling with 0s. Multiplies by $2^n$. | `5 << 1` → `10` (`0101 << 1 = 1010`) |
| `>>` | Right Shift | Shifts bits right. Divides by $2^n$ (integer division). | `5 >> 1` → `2` (`0101 >> 1 = 0010`) |

## Execution Semantics & Two's Complement

Python integers are **arbitrary-precision** (they can grow indefinitely), but they behave like signed integers using infinite **Two's Complement** representation for negative numbers.

**1. The `~` (NOT) Operator Quirk:**
Because of infinite precision, inverting `0` (`...00000`) logically produces an infinite string of `1s` (`...11111`), which represents `-1`.
Formula: `~x == -(x + 1)`

**2. Shifting Behaviors:**
-   `x << n`: Equivalent to $x \times 2^n$.
-   `x >> n`: Equivalent to $x // 2^n$ (floor division).

## Common Pitfalls

| Pitfall | Explanation |
| :--- | :--- |
| **Confusing `&` with `and`** | `&` processes bits; `and` processes boolean logic and short-circuits. |
| **Negative Shifts** | `x << -1` raises a `ValueError`. Shift count must be non-negative. |
| **Precedence** | Bitwise operators often have lower precedence than arithmetic but higher than comparison. `x & 1 == 0` parses as `x & (1 == 0)` -> `x & False` -> `0`. **Always use parentheses:** `(x & 1) == 0`. |
| **Memory usage** | Shifts on huge numbers (`1 << 1000000`) can consume massive memory/CPU. |

## Quick Summaries

**30-second version:**
Bitwise operators manipulate the underlying binary bits of integers. They are the tool of choice for setting flags, masking values, and performing efficient power-of-2 math. Remember that Python integers use infinite precision two's complement, making operations like `~` (NOT) behave mathematically as `-(x+1)`.

**One-line recall:**
**Bitwise operators = Binary-level manipulation of integers**

---

**Section:** **Bitwise Operators**
**Focus:** Manipulate integers at the bit level to optimize storage or math
**Last updated:** December 2025

---
