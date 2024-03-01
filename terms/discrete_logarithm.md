# Discrete Logarithm

In real numbers, discrete logarithm $log_ab = k$ such that $a^k = b$

It get more interesting when we consider discrete logarithm in a finite field.

For example:

$a^k \equiv b$ (mod p)

In this case, we can only apply the equation from $a^k$ side and we can't do $log_ab$.

In elliptic curve, a point $G$ "dot" with itself k times would be written as $G * k$ so we would have the same property here. That way
we can't find $k$ from known $G$ and $D$ point which $G * k = D$.

> [!NOTE] 
> We do actually have some algorithm to solve the discrete logarithm problem, but with a big enough $k$, they are not efficient
> enough to run in a reasonable timeframe. Therefore, we can consider it as negligible for the time being.

The discrete logarithm problem is believed to be computationally intractable in certain [groups](group.md) $G$. An important caveat is
that quantum computers can solve the discrete logarithm problem in polynomial time via Shor’s algorithm. Hence, cryptosystems whose
security is based on the assumed hardness of the discrete logarithm problem are not post-quantum secure.
