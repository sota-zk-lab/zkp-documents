# Lagrange Interpolation

> [!NOTE]
> We can represent any polynomial through its set of points instead of its formula.
>

> [!NOTE]
> By avoiding the conversion of points into coefficients, we can potentially reduce time complexity by $O(\log n)$.

## Univariate

Given a set of points $(x_i, y_i)$, where $i = 0, 1, 2, \ldots, n$, the Lagrange interpolating polynomial is expressed
as:

$P(x) = \sum_{i=0}^{n} y_i \cdot L_i(x)$

where $L_i(x)$ denotes the Lagrange basis polynomials, defined as:

$L_i(x) = \prod_{j=0, j \neq i}^{n} \frac{x - x_j}{x_i - x_j}$

These basis polynomials possess the property that $L_i(x_j) = \delta_{ij}$ (Kronecker delta), indicating they are 1 when
$i = j$ and 0 otherwise.

## Multilinear Lagrange Basis Polynomials

We use the notation $\tilde{f}$ for this special extension of $f$:
$\tilde{f}(x_1, ..., x_v) = \sum_{w\in \{0,1\}^v} f(w)· χ_w(x_1, ..., x_v),$
where, for any $w = (w1,...w_v)$:
$χ_w(x_1,...,x_v) := \prod_{i=1}^v (x_iw_i + (1 - x_i)(1-w_i)).$
The set $\{χ_w: w \in \{0, 1\}^v\}$ is referred to as the set of **multilinear Lagrange basis polynomials**.

### Evaluating the multilinear extension

There are two efficient methods for evaluating $\tilde f$ at any point $r \in F^v$.

#### CTY11

Fix a positive integer $v$ and let $n = 2^v$. Given input $f(w)$ for all $w \in \{0,
1\}^v$ and a vector $r \in F^{\log n}$, $V$ can compute $\tilde f(r)$ in $O(n \log n)$ time and $O(\log n)$ space.

**Proof**:
$V$ can compute $\tilde f(r)$ incrementally from the stream: $\tilde f(r) ← \tilde f(r) + f(w) · χ_w(r)$
Thus, $V$ needs to store $\tilde f(r)$ and $r$, requiring $O(\log n)$ space.

#### VSBW13

$V$ can compute $\tilde f(r)$ in $O(n)$ time and $O(n)$ space.

**Proof**:
$\tilde f(r)$ can be expressed as the inner product of two $n$-dimensional vectors, where the $w$-th entry of each is
$f(w)$
and $χ_w(r)$ respectively. To compute this in $O(n)$ with $O(n)$ space, we create $v$ stages, where the $j$-th stage
constructs a table $A^{(j)}$ of size $2^j$:
For any $(w_1,...w_j)$, we have $A^{(j)}[(w_1,...,w_j)]=\prod_{i = 1}^jχ_{w_i}(r_i)$
So, we have the following dynamic programming formula: $A^{(j)}[(w_1,...,w_j)]=A^{(j - 1)} [(w_1,...,w_{j - 1})]·(
w_jr_j + (1 - w_j)(1-r_j)$
This stage requires time $O(2^j)$. The total time is: $O\left(\sum_{j=1}^{\log n}2^j\right) = O(2^{\log n}) = O(n)$
