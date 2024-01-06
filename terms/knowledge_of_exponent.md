# Knowledge Of Exponent (KOE)

>[!Main idea]
If you get a pair of points $P$ and $Q$, where $P * k = Q$  (you don't know what $k$ is), and you get a point $C$, then it is not possible to come up
with $C * k$ unless $C$ is “derived” from $P$ in some way that you know.

Supposed that a pair of points $(P, Q)$ falls from the sky, where $P * k = Q$, but nobody knows what the value of $k$
is. Now, suppose that I come up with a pair of points $(R, S)$ where $R * k = S$. Then, the knowledge of exponent
assumption implies that the only way I could have made that pair of points was by taking $P$ and $Q$, and multiplying
both by some factor $r$ __that I personally know__.

It's equals to multiply both side of equation $P * k = Q$ by $r$ with $P * r = R, Q * r = S$ so we can have a new pair $(R, S)$ that $R * k = S$

Checking $R * k = S$ doesn’t actually require knowing k instead, you can simply check whether or not $e(R, Q) = e(P,S)$ using [elliptic curve pairings](../../terms/elliptic_curve.md#elliptic-curve-pairings). You can do that because both side have one $r$ and $k$ inside.

$$
\begin{align}
e(R, Q) &= e(P, S) \\
e(P * r, P * k) &= e(P, P * r * k) \\
e(P, P * r * k) &= e(P, P * r * k)
\end{align}
$$

Let’s do something more interesting. Suppose that we have ten pairs of points we already know: $(P_1, Q_1),(P_2,Q_2)… (P_{10}, Q_{10})$. In all cases, $P_i * k = Q_i$. Suppose we then want to know a pair of points $(R, S)$ where $R * k = S$. So if we apply the knowledge of exponent assumption here. You know that the only way that we can have $R$ is by having a linear combination $P_1 * i_1 + P_2 * i_2 + … + P_{10} * i_{10} = R$, where I know the coefficients $i_1, i_2 … i_{10}$. That is, the only way to arrive at such a pair of
points $(R, S)$ is to take some multiples of $P_1, P_2 … P_{10}$ and add them together, and make the same calculation
with $Q_1, Q_2 … Q_{10}$ with the same coefficients $i_1, i_2 … i_{10}$.

Note that, given any specific set of $P_1…P_{10}$ points that you might want to check linear combinations for, you can’t
actually create the accompanying $Q_1…Q_{10}$ points without knowing what $k$ is, and if you do know what $k$ is then
you can create a pair $(R, S)$ where $R * k = S$ for whatever $R$ you want, without bothering to create a linear
combination. ==Hence, for this to work it’s absolutely imperative that whoever creates those points is trustworthy and
actually deletes k once they created the ten points.== ==**This is where the concept of
a [trusted setup](trusted_setup.md) comes from**====.