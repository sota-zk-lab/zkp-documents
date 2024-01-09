# Polynomial Commitment

> [!NOTE]
> A [polynomial commitment](https://pdfs.semanticscholar.org/31eb/add7a0109a584cfbf94b3afaa3c117c78c91.pdf) is a
> succinct
> representation of a polynomial, enabling the verification of specific polynomial evaluations without requiring
> knowledge
> of the entire polynomial.

In simpler terms, if someone provides a commitment $c$ representing $P(x)$, they can also generate a proof convincing
you of the value of $P(z)$ for a particular $z$. (Refer
to [Reed-solomon fingerprinting](../../docs/reed_solomon_fingerprinting.md) for a related concept).

There are two crucial components to this process: the commitment to the polynomial and the opening to a value at a
specific point.

Various techniques exist for making commitments:

- [FRI (Fast Reed-Solomon Interactive Oracle) protocol](https://vitalik.eth.limo/general/2017/11/22/starks_part_2.html).
- [Kate commitments](100_kate_commitment.md).
- [Dory commitments](200_dory_commitment.md).
