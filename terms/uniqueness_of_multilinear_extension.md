# **Uniqueness of Multilinear Extension**

> [!NOTE]  
> Any function $f: \{0, 1\}^v → F$ has a unique [multilinear](multilinear.md) [extension](extension) (MLE) over $F$.

## Proof

To show that there is a unique MLE $f$. We show that if there are two multilinear polynomials over $F$: $p(x)$ = $q(x)$
for all $x \in F^v$, then $p$ and $q$ are in fact the same polynomial. Equivalently, we want to show that the polynomial
$h = p - q$ is identically 0.

We see that $h$ is also multilinear and an $h(x) = 0$ for all $x \in F^v$ (\*)

We assume that $h$ is not the identically zero polynomial. Then, we consider term $t$ in $h$ which has minimal degree.
For example, if $h(x_1,x_2, x_3) = x_1x_2x_3 + 2x_1x_2$ then $t$ is $2x_1x_2$ (degree 2).
We also consider the input $z$ obtained by setting all of the variables in $t$ to 1, and all other variables to 0 (
$z = (1, 1, 0)$ in the example). Thus, $t$ is non-zero.

However, for another terms (term $t'$), they must include at least one variable which is not in $t$ (if not, $t'$ would
either be the same as $t$ or have lower degree). So, $t'$ is zero.

Therefore, $h(z) \ne 0$, which conflicts with (\*).
So, the assumption does not exist.
