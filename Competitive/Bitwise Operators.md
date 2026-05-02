# Bitwise Operators useful in Competitive Programming

Bitwise operations are the fastest way to manipulate data, occurring directly on the CPU's registers. These are essential for "Single Number" style problems and hardware-level programming.

| Operator | Symbol | Logic | Common Use Case |
| :--- | :---: | :--- | :--- |
| **AND** | `&` | `1` if both bits are `1` | **Masking:** Checking if a specific bit is "on". |
| **OR** | `\|` | `1` if at least one bit is `1` | **Setting:** Forcing a specific bit to "on". |
| **XOR** | `^` | `1` if bits are different | **Toggling:** Canceling out identical pairs. |
| **NOT** | `~` | Flips all bits (`0`→`1`) | **Inverting:** Creating "gate" masks to block bits. |
| **L-Shift** | `<<` | Moves bits left | **Math:** Fast multiplication by powers of 2. |
| **R-Shift** | `>>` | Moves bits right | **Math:** Fast division by powers of 2. |

---
