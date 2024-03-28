# Diophantine Set

## Definition

A set $S \in \mathbb{Z}^k$ is called ==Diophantine== if and only if there exists a integer coefficient multivariate polynomial $R_S$
such that
$\mu \in S \Leftrightarrow \exists \omega \in \mathbb{Z}^{k'} s.t.\ R_S(\mu, \omega)=0$, i.e $\mu \in S$ if $\mu$ is a part of a
solution for a
fixed Diophantine equation. We call $R_S$ as a ==representing polynomial== of $S$, and $\omega$ as an auxiliary witness.

For example: The set $S$ consisting of the composite numbers is a Diophantine set with the corresponding representing polynomial $R_S(
\mu;\ \omega_1, \omega_2) = \mu - (\omega_1+1)(\omega_2+1) \ |\ \mu,\omega_1,\omega_2 \in \mathbb{N}^*$

## MRDP Theorem

Here's one of the more surprising results in mathematics:

- **Computably Enumerable Sets :** A set $S$ is _computably enumerable_ if and only if there is an algorithm that halts if the input is
  a member of $S$, and runs forever if otherwise. Equivalently, a set $S$ is _computably enumerable_ if there is an algorithm (not
  necessarily halts) that enumerates the members of $S$. Obviously, a lot of sets we deal with are computably enumerable.
- **Matiyasevich's Theorem (MRDP Theorem)** : \[Diophantine Sets] = \[Computably Enumerable Sets]

## Fact

<a id="fact"></a> Suppose we have two Diophantine sets $S_1$ and $S_2$, with respective representing polynomials $P_1,P_2$. Then:

- $R_{S_1 \cup S_2}(\mu; \omega_1, \omega_2)=P_1(\mu_1, \omega_1) \cdot P_2(\mu_2, \omega_2)$
- $R_{S_1 \cap S_2}(\mu; \omega_1, \omega_2)=P_1(\mu_1, \omega_1)^2 + P_2(\mu_2, \omega_2)^2$
