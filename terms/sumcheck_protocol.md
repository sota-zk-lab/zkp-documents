---
comments: true
---

# Sum-Check Protocol

Given a $v$-variate polynomial $g$ defined over a finite field $F$, the purpose of the sum-check protocol is for the prover to provide
this sum for the verifier:

$$
H := \sum_{b_{1} \in \{0, 1\}} \dots \sum_{b_{v} \in \{0, 1\}} g(b_{1}, \dots, b_v)
$$

**What does the verifier gain by using the sum-check protocol?**

Instead of computing $H$ via the equation above (runtime $2^v$), $V$ can use the sum-check protocol to reduce the runtime to:
$O(v + \text{the cost to evaluate } g \text{ at a single input in } F^v)$. $P$ can compute all of its prescribed messages by evaluating
$g$ at $O(2^v)$ inputs in $F^v$.

## Description of Sum-Check Protocol

- At the start of the protocol, the prover sends a value $C_1$ claimed to equal the value $H$ defined in the equation above.
- In the first round, $P$ sends the univariate polynomial $g_1(X_1)$ claimed to equal:

$$
\begin{aligned}
\sum_{(x_2, \dots, x_v) \in \{0, 1\}^{v-1}} g(X_1, x_2, \dots, x_v)
\end{aligned}
$$

$V$ checks that:

- $g_1(0) + g_1(1) = C_1$
- $g_1$ is a univariate polynomial of degree at most $\text{deg}_1(g)$, where $\text{deg}_j(g)$ is the degree of $g(X_1, X_2, \dots,
  X_v)$ in variable $X_j$.

- $V$ chooses a random element $r_1 \in F$ and sends $r_1$ to $P$.
- In the $j$-th round, for $1 < j < v$, $P$ sends to $V$ a univariate polynomial $g_j(X_j)$ claimed to equal:

$$
\begin{aligned}
\sum_{(x_{j+1}, \dots, x_v) \in \{0, 1\}^{v-j}} g(r_1, \dots, r_{j-1}, X_j, x_{j+1}, \dots, x_v)
\end{aligned}
$$

$V$ checks that:

- $g_j(0) + g_j(1) = g_{j-1}(r_{j-1})$
- $g_j$ is a univariate polynomial of degree at most $\text{deg}_j(g)$. If not, $V$ rejects.
- $V$ chooses a random element $r_j \in F$ and sends it to $P$.
- In Round $v$, after $P$ sends $g_v(X_v)$ to $V$ and $V$ checks the conditions, $V$ chooses a random element $r_v \in F$, evaluates
  $g(r_1, r_2, \dots, r_v)$, and checks that $g_v(r_v) = g(r_1, \dots, r_v)$. If not, $V$ rejects.
- If $V$ has not yet rejected, $V$ accepts.

## Completeness and Soundness

Let $g$ be a $v$-variate polynomial of degree at most $d$ in each variable, defined over a finite field $F$. The completeness error
$\delta_c = 0$ and the soundness error $\delta_s \leq vd/|F|$.

## Discussion of Costs

| Communication                     | Round | $V$ Time                                  | $P$ Time                                                |
|-----------------------------------|-------|-------------------------------------------|---------------------------------------------------------|
| $O(\sum_{i=1}^v \text{deg}_i(g))$ | $v$   | $O(v + \sum_{i=1}^v \text{deg}_i(g)) + T$ | $O(\sum_{i=1}^v \text{deg}_i(g) \cdot 2^{v-i} \cdot T)$ |

where $T$ is the cost of an oracle query to $g$.
