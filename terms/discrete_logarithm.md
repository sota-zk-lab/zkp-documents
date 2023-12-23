# Discrete Logarithm
In real numbers, discrete logarithm $log_ab = k$ such that $a^k = b$

It get more interesting when we consider discrete logarithm in a finite field.

For example:

$a^k \equiv b$ (mod p) 

In this case, we can only apply the equation from $a^k$ side and we can't do $log_ab$.

In elliptic curve, a point G "dot" with itself k times would be written as $G * k$ so we would have the same property here. That way we can't find k from known G and D point which $G * k = D$.

Discrete logarithm is the base of most algorithm security. Without it, those system would be broken in no time.