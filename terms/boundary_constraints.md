---
comments: true
---
# Boundary Constraints

Boundary constraints specify that at the start or at the end of the computation an indicated register has a given value.
We define  boundary constraints as a set $B$ of triple $(r, c, e) \in \lbrace0,..,T \rbrace \times \lbrace 0,...,w-1 \rbrace \times F$,
which means that the value of row $r$ and column $c$ is $e$ in trace.
