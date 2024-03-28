# Elliptic curve group

## Definition

You should take a look at the definition of group [here](group.md), and Elliptic curve [here](elliptic_curve.md).
## Algorithms for computing discrete logarithms

The fastest known classical algorithm to solve the Discrete Logarithm problem over
most elliptic curve groups used in practice runs in time $O(\sqrt{G})$. For example, a popular elliptic curve called Curve25519, which
is defined over base field $F$ of size $2^{255} −19$, defines a cyclic group of order close to $2^{252}$, so the time complexity is
about $O(2^{128})$.  
## Scalar field vs base field

The [base field](base_field.md) is used to represent points on a curve while the [scalar
field](scalar_field.md) allows performing scalar multiplication on those points.
