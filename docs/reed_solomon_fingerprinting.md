# Reed-Solomon Fingerprinting

`rid-'solomon`

In Reed-Solomon Fingerprinting, Alice optimizes data transfer by sending only hashes to Bob instead of
the entire file. The integrity check involves comparing hash values, providing Bob with a high level of confidence in
the equality of files.

The hash function used in this protocol is denoted as $p_a(x)= \Sigma^n_{i=1} a_i · x^{i−1}$, referred to as
Reed-Solomon encoding.

In this context, the [Fundamental theorem of Algebra](../terms/fundamental_theorem_of_algebra.md) is leveraged to
imply the following:

> For any two distinct (unequal) polynomials $p_a$ and $p_b$ of degree at most $n$ with coefficients in $\mathbb{F}_p$,
> $p_a(x) = p_b(x)$ for at most $n$ values of $x$ in $\mathbb{F}_p$.

> [!NOTE]
> Any input can be represented by a polynomial.
>
> Comparing the evaluations of their respective polynomials at a random
> point allows us to check whether two inputs are identical.
>
> The probability of these two evaluations being the same, even when their inputs differ, is given by $(n-1)/p$, which
> approaches 0 when $p >> n$.

| Symbol           | Definition                     | Note                |
|------------------|--------------------------------|---------------------|
| $a$              | Alice's file                   |                     |
| $b$              | Bob's file                     |                     |
| $n$              | number of characters           |                     |
| $m$              | number of possible characters  |                     |
| $a_1$,..., $a_n$ | Alice's characters             |                     |
| $b_1$,..., $b_n$ | Bob's characters               |                     |
| $H$              | hash functions family          |                     |
| $h(x)$           | hash function                  |                     |
| $p$              | modulo                         | $p\geq\max(m, n^2)$ |
| $\mathbb{F}_p$   | finite field over $p$          |                     |
| $r$              | random value in $\mathbb{F}_p$ |                     |
| $v$              | $h_r(a)$                       |                     |
