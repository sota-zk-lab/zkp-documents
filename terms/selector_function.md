# Selector Function

A selector function, denoted as $f(x)$, serves as an alternative representation of an array $A=[a_0, a_2, ..., a_n]$,
where $f(0) = a_0, f(1) = a_1, ..., f(n) = a_n$. This representation is achieved
through [Lagrange interpolation](lagrange_interpolation.md).

The primary purpose of a selector function is to "compress" multiple checks into a single operation. For instance,
consider the need to verify an equation such as $a_i + b_i = c_i$. In this scenario, three selectors $A(x)$, $B(x)$, and
$C(x)$ can be created, and the validation can be expressed as:

$$A(x) + B(x) = C(x)$$

This approach streamlines the verification process by consolidating multiple checks into a more efficient single
operation.
