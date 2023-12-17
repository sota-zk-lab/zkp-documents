# Homogeneous Polynomial or Projective Model

## Definition

A homogeneous polynomial is a polynomial in which **every term has the same total degree**. For example, $x^2 + 2xy +
y^2$ is a homogeneous polynomial of degree 2.

To homogenize a polynomial:

$$
F^*(X,Y,Z) = Z^d F\left(\frac{X}{Z}, \frac{Y}{Z}\right) \quad \text{where } d = \text{deg}(F)
$$

## Example

Given $F(x, y) = 3x^3 - 2xy + 5y^2$:

- $d = \text{deg}(F) = 3$
- $F^*(x, y, z) = z^d F\left(\frac{x}{z}, \frac{y}{z}\right)$

Substitute the values:

$$
F^*=
z^3\left[3\left(\frac{x}{z}\right)^3 - 2\left(\frac{x}{z}\right)\left(\frac{y}{z}\right) + 5\left(\frac{y}{z}\right)^2\right]
$$

Simplify:

$$
F^*= 3x^3 - 2xyz + 5y^2z
$$