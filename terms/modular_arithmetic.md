# Modular Arithmetic

## Definition

**Modular arithmetic** is a branch of mathematics that deals with operations on numbers where the answer is confined to a fixed range.

## Basics

### Modulus Operator:
It returns the remainder when one number is divided by another.
  - Example: $13 \mod 5$ is 3 because $13 = 5 \cdot 2 + 3$.

### Congruence:
Two numbers are said to be congruent modulo $m$ if they have the same remainder when divided by $m$.
  - Example: $7 \equiv 1 \pmod{3}$ because both have a remainder of 1 when divided by 3.

## Arithmetic Operations

### Addition:
- $(a + b) \mod m = ((a \mod m) + (b \mod m)) \mod m$

### Subtraction:
- $(a - b) \mod m = ((a \mod m) - (b \mod m) + m) \mod m$

### Multiplication:
- $(a \cdot b) \mod m = ((a \mod m) \cdot (b \mod m)) \mod m$

## So why on earth is that helpful?

It turns out that if we use modulo arithmetic, having a result of operation it is non-trivial to go back to the original numbers 
because many different combinations will have the same result. Moreover, the common arithmetic properties are preserved.
