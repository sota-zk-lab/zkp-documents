# Scalar field

In the context of [elliptic curve group](elliptic_curve_group.md), **scalar field** $F_r$ is the field of scalars used in the
operations performed on the curve, such as point addition, scalar multiplication, and pairing. The **scalar field size** $r$ is also
the size of the largest subgroup of prime order. Interestingly, the Elliptic Curve DLP (ECDLP) of an elliptic curve is only as hard as
that curve's largest prime order subgroup, not its order. However, when curve's order is prime, its largest prime subgroup is the group
itself, so $r$ is also the order of the group.
