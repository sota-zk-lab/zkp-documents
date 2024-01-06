---
Title: Bird’s Eye View of Practical Arguments
Status: In Progress
Level: "6"
---
# Chapter 19: Bird’s Eye View of Practical Arguments

![](attachments/taxonomy.png)

## 19.1 A Taxonomy of SNARKs

Outside of the **linear-PCP-based SNARKs**, most known **SNARKs** are obtained by combining some **IP**,  **MIP**, or **constant-round polynomial IOP** with a **polynomial commitment** scheme. 
For example:

| Polynomial IOP approaches      | Polynomial Commitment Approaches                                                     | SNARK                                            |
| ------------------------------ | ------------------------------------------------------------------------------------ | ------------------------------------------------ |
| IPs                            | FRI-based (multilinear) polynomial commitments                                       | Virgo                                            |
| IPs                            | Discrete-log-based (multilinear) polynomial commitments (Bulletproofs, Hyrax-commit) | Hyrax                                            |
| IPs                            | KZG-based (multilinear) polynomial commitments                                       | zk-vSQL and Libra                                |
| MIPs                           | Multilinear polynomial commitments                                                   | Spartan, Xiphos, Kopis, Brakedown, and Shockwave |
| Constant-round polynomial IOPs | FRI-based (univariate) polynomial commitments                                        | Aurora, Fractal, and Redshift                    |
| Constant-round polynomial IOPs | KZG-based (univariate) polynomial commitments                                        | Marlin                                           |
| Constant-round polynomial IOP  | Ligero                                                                               | Ligero                                           | 

Beside that, the most popular variant of the SNARK derived from GGPR’s linear PCP is
Groth16.


**More SNARKs via composition**: On top of the taxonomy of SNARKs delineated above, one can take any two SNARKs designed via one of the above approaches, and compose them one or more times. Such compositions are growing increasingly popular and already yield state-of-the-art performance.

**Pros and cons of three first approach in section 10.6**.

a fifth approach to argument design, based on commit-and-prove techniques (13.1) (not so related)

 (IP-based, MIP-based, and constant-round-polynomial-IOP-based) 


 the information-theoretically secure protocol 
 +
 any extractable polynomial commitment scheme
 =
  succinct argument


Only one technique to to turn linear PCPs into publicly-verifiable SNARKs, based on pairings and very similar to KZG polynomial commitments,



IP-based and MIP-based argument systems, the polynomial commitment scheme must allow committing to multilinear polynomials.

the IOP-based argument system, the polynomial commitment scheme must allow committing to univariate polynomials

three broad **approaches** to polynomial commitment schemes 
	some of these approaches have multiple instantiations with various cost tradeoff

	IOPs combined with Merkle hashing, where we saw FRI

	transparent Σ-protocols that assume hardness of the discrete logarithm problem, where we saw Hyrax-commit (Section 14.3), Bulletproofs (Section 14.4), and Dory

	KZG [KZG10] and uses pairings and a trusted setup (Section 15.2)

    = 
	“IOP- based”, “discrete-log-based”, and “KZG-based”.


**pros and cons of the various polynomial commitment schemes in Section 16.3.**





SNARKs via composition
	As discussed in Section 18.1, by taking a “fast-prover, larger-proof” SNARK and composing it with a “slower prover-smaller proof” SNARK, one can in principle obtain a “best-of-both-worlds” SNARK with a fast prover and small proofs.


## 19.2 Pros and Cons of the Approaches

### Approaches Minimizing Proof Size
There are 2 approaches that achieve proofs consisting of a constant  
number of group elements:
1. Linear PCPs: smallest proof size (3 group elements).
2. constant-round polynomial IOPs combined with KZG-based polynomial commitments.
The downsides of these are:
1. They both require a trusted setup. For [SRS](../../terms/structured_reference_string.md), it is universal and updatable for (2), computation-specific for (1).
2. Computationally expensive for the prover.

**Transparency**: (depend on the polynomial commitment scheme)

All of the remaining approaches are transparent unless they choose to use KZG-based polynomial commitments. They use uniform reference string (URS) rather than a [SRS](../../terms/structured_reference_string.md), and hence no toxic waste is produced.

**Post-quantum security**: 
The approaches that are plausibly post-quantum secure are comprised of those  
that utilize an IOP-based polynomial commitment (FRI, Ligero, Brakedown).

The others are not due to their reliance on the hardness of discrete log.

**Dominant contributor to cost: polynomial commitments**
Normally, the polynomial commitment dominates the most relevant costs: prover time, proof length, and verifier time when combined with MIPs and constant-round polynomial IOPs.  

There is an exception that, if an MIP is combined with KZG commitments, it is the MIP and not the polynomial commitment that dominates verification costs).

Here is a brief summary of how concrete costs compare. Prover costs:
1. FRI and Bulletproofs are the most expensive polynomial commitment schemes.
2. Pairings (Dory and KZG commitments). 
3. Hyrax, Ligero and Brakedown’s commitments are similar
4.  Brakedown is slightly faster. 

Commitment size and evaluation proof length:
1. Brakedown > Ligero > Hyrax: roughly square-root size proofs.
2. FRI: polylogarithmic proof size.
3. Dory and Bulletproofs: logarithmic size proofs. 
4. KZG-commitments for univariate polynomials (constant size).

**Constant-round IOPs vs. MIPs and IPs.**

**Constant-round IOPs**:  much slower and more space intensive for the prover because they require to commit to many polynomials ($\ge 10$), while in **MIPs and IPs**, prover needs to commit only single polynomial.

**On pre-processing and work-saving for the verifier**
The approaches requiring an [SRS](../../terms/structured_reference_string.md) inherently require a pre-processing phase to  
generate the SRS and this take time proportional to the size of the circuit.

	“paying for” an expensive pre-processing phase can enable improved verification costs in the online phase of the protocol



**Prover time in holographic vs. non-holographic SNARKs**
Non-holographic systems may achieve faster prover time as measured on a per-gate basis, but they may have to use much bigger circuits.

## 19.3 Other Issues Affecting Concrete Efficiency

### 19.3.1 Field Choice
The designer’s choice of field to work over can be limited:
1. Many cryptographic applications naturally work over fields that do not satisfy the  
properties required by many SNARKs.
2. For certain fields, addition and multiplication are particularly efficient on modern computers.