# Coordinate Pair Accumulator

> [!NOTE]
> If two points share the same Y value, swapping them does not change the result of $p(x)$.

## Scheme

The coordinate pair accumulator $p(x)$ is defined as:

$$p(x + 1) = p(x) \cdot (\upsilon_1 + X(x) + \upsilon_2 \cdot Y(x))$$

- $X(x)$ and $Y(x)$ are two polynomials representing the $x$ and $y$ coordinates of a set of points.
- $\upsilon_1$ and $\upsilon_2$: random constants
- $p(0) = 1$

When we swap $X$ in positions where they have the same $Y$ value (e.g., when $x = 1,3$), the value of $p(x)$ remains
unchanged. Thus, we can verify if two positions share the same Y value by checking if $p(x)$ retains its value after the
permutation.

## Example

Let $\upsilon_1 = 3$ and $\upsilon_2 = 2$, we have:

| $x$                                         | $0$  | $1$  | $2$  | $3$   | $4$    |
|---------------------------------------------|------|------|------|-------|--------|
| $X(x) = x$                                  | $0$  | $1$  | $2$  | $3$   |        |
| $Y(x) = x^3 - 5x^2 + 7x - 2$                | $-2$ | $1$  | $0$  | $1$   |        |
| $\upsilon_1 + X(x) + \upsilon_2 \cdot Y(x)$ | $-1$ | $6$  | $5$  | $8$   |        |
| $p(x)$                                      | $1$  | $-1$ | $-6$ | $-30$ | $-240$ |

| $x$                                            | $0$  | $1$     | $2$ | $3$     |
|------------------------------------------------|------|---------|-----|---------|
| *Before*                                       |      |         |     |         |
| $X(x) = x$                                     | $0$  | ==$1$== | $2$ | ==$3$== |
| $Y(x)$                                         | $-2$ | ==$1$== | $0$ | ==$1$== |
| *After*                                        |      | ....    |     |         |
| $X(x) = \frac{2}{3}x^3 - 4x^2 + \frac{19}{3}x$ | $0$  | $3$     | $2$ | $1$     |
| $Y(x)$                                         | $-2$ | $1$     | $0$ | $1$     |
