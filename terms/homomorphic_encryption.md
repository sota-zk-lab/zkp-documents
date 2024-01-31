# Homomorphic Encryption

## Definition

**Homomorphic Encryption** refers to a cryptographic technique that enables the encryption of a value while preserving the ability to perform arithmetic operations on the encrypted data without decrypting it.

## Example

Consider the following example:

### 1. Initialization:
- Select a base natural number $g$ (e.g., 5).
- Choose a value to encrypt (e.g., 3).
- Encrypt the value by exponentiating $g$ to the power of the chosen value:
  $$5^{3} = 125$$

### 2. Arithmetic Operations on Encrypted Data:
- **Multiplication (Mul):**
$$125^2 = 15625 = (5^3)^2 = 5^6$$
- **Addition (Add):**
$$5^3 \cdot 5^2 = 5^{3+2} = 5^5 = 3125$$
- **Subtraction (Sub):**
$$\frac{5^5}{5^3} = 5^5 \cdot 5^{-3} = 5^2 = 25$$


In this simple example, the public nature of the base makes it relatively easy to deduce the original secret number.
Advanced homomorphic encryption schemes address such vulnerabilities for real-world applications.
