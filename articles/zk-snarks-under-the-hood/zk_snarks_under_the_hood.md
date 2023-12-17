---
Title: "Zk-SNARKs: Under the Hood"
Status: Done
Level: 6
Note: There is a few places that are hard to fully understand
---

# Zk-SNARKs: Under the Hood

[Site](https://medium.com/@VitalikButerin/zk-snarks-under-the-hood-b33151a013f6)

[Pinocchio protocol](https://eprint.iacr.org/2013/279.pdf) Parno, Gentry, Howell and Raykova from 2013 (often called
PGHR13)

Supposed that a pair of points $(P, Q)$ falls from the sky, where $P * k = Q$, but nobody knows what the value of $k$
is. Now, suppose that I come up with a pair of points $(R, S)$ where $R * k = S$. Then,
the [knowledge of exponent](../../terms/knowledge_of_exponent.md) assumption implies that the only way I could have made
that pair of points was by taking $P$ and $Q$, and multiplying both by some factor r_that I personally know_.

Checking $R * k = S$_doesn’t actually require knowing k -_instead, you can simply check whether or not $e(R, Q) = e(P,
S)$ [elliptic curve pairings](../../terms/elliptic_curve.md#elliptic-curve-pairings)

Let’s do something more interesting. Suppose that we have ten pairs of points fall from the sky: $(P_1, Q_1), (P_2,
Q_2)… (P_{10}, Q_{10})$. In all cases, $P_i * k = Q_i$. Suppose that I then provide you with a pair of points $(R, S)$
where $R * k = S$. What do you know now? You know that $R$ is some linear combination $P_1 * i_1 + P_2 * i_2 + … + P_
{10} * i_{10}$, where I know the coefficients $i_1, i_2 … i_{10}$. That is, the only way to arrive at such a pair of
points $(R, S)$ is to take some multiples of $P_1, P_2 … P_{10}$ and add them together, and make the same calculation
with $Q_1, Q_2 … Q_{10}$.

Note that, given any specific set of $P_1…P_{10}$ points that you might want to check linear combinations for, you can’t
actually create the accompanying $Q_1…Q_{10}$ points without knowing what $k$ is, and if you do know what $k$ is then
you can create a pair $(R, S)$ where $R * k = S$ for whatever $R$ you want, without bothering to create a linear
combination. ==Hence, for this to work it’s absolutely imperative that whoever creates those points is trustworthy and
actually deletes k once they created the ten points.== ==**This is where the concept of a “trusted setup” comes from
**====.==

Remember that the solution to a QAP is a set of polynomials $(A, B, C)$ such that $A(x) * B(x) - C(x) = H(x) * Z(x)$,
where:

- A is a linear combination of a set of polynomials {$A_1…A_m$}
- B is the linear combination of {$B_1…B_m$} with the same coefficients
- C is a linear combination of {$C_1…C_m$} with the same coefficients

However, in most real-world cases, $A$, $B$ and $C$ are extremely large; for something with many thousands of circuit
gates like a hash function, the polynomials (and the factors for the linear combinations) may have many thousands of
terms. Hence, instead of having the prover provide the linear combinations directly, we are going to use the trick that
we introduced above to have the prover prove that they are providing something which is a linear combination, but
without revealing anything else.

You might have noticed that the trick above works on elliptic curve points, not polynomials. Hence, what actually
happens is that we add the following values to the trusted setup:

- $G * A_1(t), G * A_1(t) * k_a$
- $G * A_2(t), G * A_2(t) * k_a$
- …
- $G * B_1(t), G * B_1(t) * k_b$
- $G * B_2(t), G * B_2(t) * k_b$
- …
- $G * C_1(t), G * C_1(t) * k_c$
- $G * C_2(t), G * C_2(t) * k_c$

$t$ as a “secret point” at which the polynomial is evaluated. $G$ is a “generator”

$t$, $k_a$, $k_b$ and $k_c$ are "toxic waste", numbers that absolutely must be deleted at all costs

Now, if someone gives you a pair of points $P$, $Q$ such that $P * k_a = Q$ (reminder: we don’t need $k_a$ to check
this, as we can do a pairing check) then you know that **what they are giving you is a linear combination of $A_i$
polynomials evaluated at $t$**

Hence, so far the prover must give:

- $π_{a} = G * A(t)$, $π’_a = G * A(t) * k_a$
- $π_b = G * B(t)$, $π’_b = G * B(t) * k_b$
- $π_c = G * C(t)$, $π’_c = G * C(t) * k_c$

The next step is to make sure that all three linear combinations have the same coefficients. This we can do by adding
another set of values to the trusted setup: $(A_i(t) + B_i(t) + C_i(t))$, $G * (A_i(t) + B_i(t) + C_i(t)) * b$, where
$b$ is another number that should be considered "toxic waste" and discarded as soon as the trusted setup is completed.

We can then have the prover create a linear combination with these values with the same coefficients, and use the same
pairing trick as above to verify that this value matches up with the provided A + B + C.

Finally, we need to prove that $A * B - C = H * Z$. We do this once again with a pairing check:

$e(π_a, π_b) / e(π_c, G) ?= e(π_h, G * Z(t))$

$e(π_a, π_b) / e(π_c, G)=\frac{10^{π_a*π_b}}{10^{π_{c}}} = 10^{π_a*π_b-π_c}$

$e(π_h, G * Z(t)) = e(π_h, π_z) = 10^{π_{h}*π_z}$

$π_a*π_b-π_c =π_{h}*π_{z}$

- $G * A_1(t), G * A_1(t) * k_a$
- $G * A_2(t), G * A_2(t) * k_a$
- …
- $G * B_1(t), G * B_1(t) * k_b$
- $G * B_2(t), G * B_2(t) * k_b$
- …
- $G * C_1(t), G * C_1(t) * k_c$
- $G * C_2(t), G * C_2(t) * k_c$


- $π_{a} = G * A(t)$, $π’_a = G * A(t) * k_a$
- $π_b = G * B(t)$, $π’_b = G * B(t) * k_b$
- $π_c = G * C(t)$, $π’_c = G * C(t) * k_c$

$G * (A_i(t) + B_i(t) + C_i(t)) * b$

$A(X) = c_1 \cdot A_1(X) + c_2 \cdot A_2(X) + \ldots + c_k \cdot A_k(X)=>π_{a}$
$B(X) = c_1 \cdot B_1(X) + c_2 \cdot B_2(X) + \ldots + c_k \cdot B_k(X)=>π_{b}$
$C(X) = c_1 \cdot C_1(X) + c_2 \cdot C_2(X) + \ldots + c_k \cdot C_k(X)=>π_{c}$

G, G * t, G * t², G * t³, G * t⁴ ….
\

We saw above how to convert A, B and C into elliptic curve points; G is just the generator (ie. the elliptic curve point
equivalent of the number one). We can add $G * Z(t)$ to the trusted setup. H is harder; H is just a polynomial, and we
predict very little ahead of time about what its coefficients will be for each individual QAP solution. Hence, we need
to add yet more data to the trusted setup; specifically the sequence:

$G, G * t, G * t^2, G * t^3, G * t^4 ….$