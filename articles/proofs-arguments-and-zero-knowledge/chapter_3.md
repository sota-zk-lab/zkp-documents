---
Title: Definitions and Technical Preliminaries
Status: Done
Level: "3"
---

# Chapter3 - Definitions and Technical Preliminaries

## 3.1 Interactive Proofs

In an interactive proof, the Prover (**P**) claims having a value $y = f(x)$. To validate this claim, the Verifier (**V
**) exchanges a series of messages with **P**. At the conclusion of this protocol, **V** must output either 0 or 1,
where 1 indicates acceptance of the prover's claim ($y = f(x)$) and 0 indicates rejection. The entire sequence of k
messages $t := (m_1, m_2, ..., m_k)$ exchanged by **P** and **V**, along with the claimed answer y, is termed a
==transcript==.

The output of verifier $V$ on input $x$ during interaction with a deterministic prover strategy **P**, with V's internal
randomness equal to $r$, is denoted as $Out(V,x,r,P) \in \{0,1\}$.

An interactive proof system (V,P) is considered to have completeness error $δ_c$ and soundness error $δ_s$:

- [Completeness](../../terms/zkp#completeness) error $δ_c$: $\text{Pr}[\text{out}(V, x, r, P) = 1]$ $\ge$ 1 - $δ_c$
- [Soundness](../../terms/zkp.md#soundness) error $δ_s$: $\text{Pr}[\text{out}(V, x, r, P') = 1]$ $\le$ $δ_s$, where
  $P'$ is a prover strategy with value $y \ne f(x)$ (*statistical soundness*).

An interactive proof system is deemed valid if $δ_c$ and $δ_s$ are both ≤ 1/3.

## 3.2 Argument Systems

**Definition**: Read [here](../../terms/arguments.md).

## 3.3 Robustness of Definitions and the Power of Interaction

- Any [IP](../../terms/ip.md) for a function $f$ with $δ_c$ ≤ 1/3 can be transformed into perfect completeness ($δ_c$ =
  0), with a polynomial blowup in the verifier’s costs.
- Soundness Error: $1 / |F|$, where $F$ is the field over which the interactive proof is defined.

### Interactive Proofs for Languages Versus Functions

The standard requirements of an IP for the [language](../../terms/language.md) $L$ are:

- Completeness: For any $x \in L$, some prover strategies will cause the verifier to accept with high probability.
- Soundness: For any $x \notin L$, then for every prover strategy, the verifier rejects with high probability.

These properties do not necessitate convincing refutations (convincing proofs of falsity) for *false statements* (inputs
not in the language).

### NP and IP

Refer to the definitions here: [IP](../../terms/ip.md) and [NP](../../terms/np.md).

### 3.4 Schwartz-Zippel Lemma

Read the lemma [here](../../terms/schwartz_zippel_lemma.md).

### 3.5 Low Degree and Multilinear Extensions

Read the definitions of [Multilinear](../../terms/multilinear.md) and [Extension](../../terms/extension).

**Fact 3.5**: Any function $f: \{0, 1\}^v → F$ has a unique multilinear extension (MLE) over $F$. The proof is
available [here](../../terms/uniqueness_of_multilinear_extension.md).

We use the notation $\tilde{f}$ for this special extension of $f$:
$$\tilde{f}(x_1, ..., x_v) = \sum_{w\in \{0,1\}^v} f(w)· χ_w(x_1, ..., x_v), $$
where, for any $w = (w_1,...w_v)$:
$$χ_w(x_1,...,x_v) := \prod_{i=1}^v (x_iw_i + (1 - x_i)(1-w_i)). $$
The set $\{χ_w: w \in \{0, 1\}^v\}$ is referred to as the set of
==*multilinear [Lagrange basis polynomials](../../terms/lagrange_interpolation.md)*==.
