# Kate Commitment (KZG)

In response to the challenges posed in the [polynomial commitment](000_polynomial_commitment.md) context, the Kate
Commitment (KZG) scheme is introduced.

To prove that $P(z) = a$, the approach involves proving that $\frac{P(x) - a}{x - z}$ is a polynomial.

The trusted-setup procedure generates a set of [elliptic curve](../elliptic_curve.md) points $G, G \cdot s, G \cdot s^2,
\ldots, G \cdot s^n$, along with $G_2 \cdot s$, where $G$ and $G_2$ represent the generators of two elliptic curve
groups. Importantly, the secret $s$ is forgotten after the setup is completed. These points are disclosed and
collectively considered as the "**proving key**" of the scheme. Any party requiring a polynomial commitment must use
these points.

> [!NOTE]
> A commitment to a polynomial of
> degree $d$ involves multiplying each of the first $d+1$ points in the proving key by the corresponding coefficient in
> the polynomial and summing the results.

For instance, $x^3 + 2x^2+5$ is represented by $(G \cdot s^3) + 2 \cdot (G \cdot s^2) + 5 \cdot G$.

This representation provides an "evaluation" of the polynomial at $s$, without revealing $s$.

The notation $[P]$ is used to
denote $P$ encoded in this manner (i.e., $G \cdot P(s)$). [Elliptic curve pairings](../elliptic_curve_pairings.md) can
be used to check that $e([P] - G \cdot a, G_2) = e([Q], [x] -
G_2 \cdot z)$ as a means of verifying $P(x) - a = Q(x) \cdot (x - z)$.
