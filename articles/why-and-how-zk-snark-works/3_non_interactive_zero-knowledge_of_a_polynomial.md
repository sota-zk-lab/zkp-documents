---
Title: Non interactive Zero-knowledge of a polynomial
Status: Done
Level: "3"
---
# Chapter 3 - Non-Interactive Zero Knowledge of a Polynomial

## 3.1. Proving Knowledge of a Polynomial

We initiate our exploration with the challenge of proving knowledge of a polynomial, gradually developing a generic approach and 
uncovering various properties of polynomials along the way.

Thus far, our discussions have centered on a rudimentary notion of proof, lacking mechanisms to enforce protocol rules. For instance, 
the prover may not necessarily be acquainted with the polynomial and could employ alternative methods to yield a correct result. 
Additionally, if the verifier's polynomial evaluations have a limited amplitude, such as 10, the verifier might guess a number with a 
non-negligible probability of acceptance. Addressing these weaknesses becomes imperative, but first, let's delve into what it truly 
means to "know" a polynomial.

## 3.2. **Factorization**

It states that any polynomial can be factored into linear polynomials as long as it is solvable. See the [lagrange interpolation](../../terms/lagrange_interpolation.md) for more informations.

Example:
$$(x - a_{0})(x - a_{1})...(x - a_{n}) = 0$$

[Define](./notes.md) *p(x)* as a sample polynomial, and *p(x)* is the multiplication of those cofactors *t(x)*. So we have arbitrary
polynomial:

$$h(x) = \frac{p(x)}{t(x)}$$

In particular:

Given:
$$p(x)  = x^3 - 3x^2 + 2x$$

$$t(x) = (x-1)(x-2)$$

- The Verifier samples a random value 23, calculates:
 $$t = t(23) = (23 - 1)(23 - 2) = 462$$ And gives 23 to the Prover.

- The Prover calculates $h(x) = \frac{p(x)}{t(x)}$ and evaluates
 $$p = p(23) = 10626$$  
 $$h = h(23) = 23$$ And provides $p, h$ to the Verifier.

- The Verifier then checks that:  $$p = t \cdot h = 10626 = 462 \cdot 23$$

   
If this statement holds true, it implies that the prover provided an accurate polynomial.

> [!Summary]
> Prover may not know the claimed polynomial $p(x)$ at all.
>
> In the current protocol there is no enforcement of degree. Hence prover can cheat by using a polynomial of higher degree which also
> satisfies the cofactors check.
>
> Because prover knows the random point $x = r$, he can construct any polynomial which has one shared point at $r$ with $t(r) · h(r)$.

## 3.3 Obscure Evaluation

Due to the information revealed in its raw form, the prover possesses knowledge of both the sample random value $r$ and its
corresponding transformed value $t(r)$, which should remain concealed. Consequently, a mechanism akin to a hash function must be
employed a process that, once executed, renders it challenging to reverse-engineer the original input.

### 3.3.1 Homomorphic Encryption

See the [Homomorphic Encryption](../../terms/homomorphic_encryption.md).

### 3.3.2 Modular Arithmetic

See the [Modular Arithmetic](../../terms/modular_arithmetic.md).

### 3.3.3 Strong Homomorphic Encryption

We use Modular Arithmetic for Homomorphic Encryption.

### 3.3.4. Encrypted Polynomial

Let's define $E$ :
$$E(x) = g^{v} \pmod{n}$$
As $v$ is monomial of polynomial.

For example, we have:
$$p(x) = x^{3} - 3x^{2} + 2x$$

In this case, with coefficients 1, -3, 2, the encrypted polynomial can be evaluated as follows:

$$
\begin{aligned}
E(x^{3})^{1}E(x^{2})^{-3}E(x)^{2}= \\
 (g^{x^{3}})^{1}(g^{x^{2}})^{-3}(g^{x})^{2}= \\
 g^{1x^{3}-3x^{2}+2x}= \\
 g^{x^{3}-3x^{2}+2x} \\
\end{aligned}
$$

*Verifier*:

- Generate a random *s*.
- Calculate $E(s^{i}) = g^{s^{i}}$: same as the example above.
- Evaluate the *target polynomial* with *s*: *t(s)*.
- Provide to the Prover: $E(s^{0}),E(s^{1}),E(s^{2}),...,E(s^{d})$.

*Prover*:

- Calculates $h(x) = \frac{p(x)}{t(x)}$  *we just calculate the polynomial $h(x)$ in here*.  
- Evaluates: $E(p(s))$, $E(h(s))=g^{h(s)}$.
- Provides $g^{p}$, $g^{h}$.

*Verifier*:

- Check that $p=t(s) \cdot h$, meaning:
  $$g^{p} = (g^{h})^{t(s)}$$

If the Prover claims to have a satisfactory polynomial using only 2 powers $s^{3}$ and $s^{1}$, it is not possible to verify in the
current protocol.

## 3.4. Restricting a Polynomial

The main idea to resolve above problem is to sample a random $\alpha$, and the provider needs to calculate
$a^{,} = a^{\alpha} \pmod{n}$, then provide the tuple $(a,a^{,})$ using an [elliptic curve](../../terms/elliptic_curve.md). This
ensures that the provider can't extract $\alpha$ from the tuple $(a,a^{,})$ through *brute force*, it also called
[Knowledge of exponent](../../terms/knowledge_of_exponent.md).

We can also apply this construction with the simple one-coefficient polynomial:
$$f(x)= c \cdot x$$

The Verifier can now check the equality:  $(a^{c})^{\alpha} = (\alpha^{,})^{c}$

In summary:

*Verifier*:

- Chooses 2 random *s*, $\alpha$ and provides evaluations for $x=s$ and
- $(g^{s},g^{\alpha \cdot s})$
*Prover*: Applies the coefficient $c$:  
$((g^{s})^c,(g^{\alpha \cdot s})^{c})=(g^{c \cdot s},g^{\alpha \cdot s \cdot c})
$
- *Verifier*: Checks

In particular, for a degree $3$ polynomial:
$$p(x) = x^{3} - 3x^{2} + 2x$$

*Verifier*:

- Provides encrypted: $g^{s^{0}},g^{s^{1}}, \cdots,g^{s^{d}}$ and their *shifts*
$g^{\alpha s^{0}},g^{\alpha s^{1}}, \cdots,g^{\alpha s^{d}}$

*Prover*:

- Evaluates the encrypted polynomial with $s$:

$$
\begin{aligned}
 g^{p} = g^{p(s)} =(g^{s_{0}})^{c_{0}} \cdot (g^{s_{1}})^{c_{1}} \cdots
(g^{s_{d}})^{c_{d}}
 \\ = g^{c_{0}s^{0} +c_{1}s^{1}+ \cdots+c_{d}s^{d}  }
=g^{s^{3}} \cdot g^{-3s^{2}} \cdot g^{2s}=g^{s^{3}-3s^{2}+2s}
\end{aligned}
$$

$$\Rightarrow g^{{p}'} = g^{\alpha (s^{3}-3s^{2}+2s)}$$
*Verifier* checks :
  $$(g^{p})^{\alpha}=g^{{p}'}$$
  $$\Rightarrow (g^{s^{3}-3s^{2}+2s})^{\alpha} = g^{\alpha (s^{3}-3s^{2}+2s)}$$

> [!Conclusion]
>
> We can be sure that the Prover did not use anything else other than the polynomial provided by the Verifier since there is no other
> way to preserve $\alpha$.
>
> *The Verifier possesses the capability to exhaustively attempt a constrained set of coefficient combinations until achieving a result
> that matches the Prover's response.* Consequently, the protocol can no longer be classified as zero knowledge.
>
> Moreover, the secure protocol should be secure even in cases where there is only one coefficient, and its value is 1.

## 3.5. Zero-Knowledge

Because the Verifier can extract knowledge about the unknown polynomial $p(x)$ only from the data sent by the Prover. So we can *shift*
$g^{p}$, $(g^{p})^{\alpha}$ by a random number $\delta$.

## 3.6. Non-Interactivity

Up to this point, the proof is only valid for the original Verifier because:

- The Verifier could collude with the Prover and disclose those secret parameters $s,\alpha$.
- The Verifier has to store $\alpha$ and $t(s)$ until all relevant proofs are verified.

Hence, we need to secure the secrets $(t(s),\alpha)$, and this is where [cryptographic pairing](../../terms/elliptic_curve_pairings.md)
fits in.

### 3.6.1. Multiplication of Encrypted Values

[Cryptographic pairings](../../terms/pairings_or_bilinear_map.md) (bilinear map) have the core properties that can be expressed as:
$$e(g^{a},g^{b})=e(g^{b},g^{a})=e(g^{ab},g^{1})=e(g^{1},g^{ab})=e(g^{1},
g^{a})^{b}=e(g^{1},g^{1})^{ab}= \cdots$$

### 3.6.2. Trusted Party Setup

We trust a single party to generate secrets $s$ and $\alpha$. As soon as $\alpha$ and all necessary powers of $s$ with *shift* are
encrypted, they must be deleted. So we use a [common reference string](../../terms/common_reference_string.md) or **CRS** to
generate these parameters.

### 3.6.3. Trusting One out of Many

There is no way to prove that $\alpha$ and $s$ are deleted. So we can generate a composite
[CRS](../../terms/common_reference_string.md) by multiple parties.

In particular:

- Alice samples her random $s_{A}$ and $\alpha_{A}$ and publishes her CRS: $g^{s_{A}^{i}},g^{\alpha_{A}},g^{\alpha_{A}s_{A}^{i}}$  
- Bob samples his $s_{B}$ and $\alpha_{B}$ and  Alice's CRS through homomorphic  multiplication: $(g^{s_{A}^{i}})^{s_{B}^{i}},(g^
  {\alpha_{A}})^{\alpha_{B}},
(g^{\alpha_{A}s_{A}^{i}})^{\alpha_{B}s_{B}^{i}}$, then publishes A-B's CRS:
$(g^{s_{AB}^{i}},g^{\alpha A B},g^{\alpha_{AB}s_{AB}^{i}})$
- So does with C, D, E, $\cdots$.

> [!Conclusion]
>  
> *The more there are unrelated participants in [CRS](../../terms/common_reference_string.md) setup, the fainter the possibility
> of fake proofs*.

## 3.7. Succinct Non-Interactive Argument of Knowledge of Polynomial

Denote ${s^{i}}_{i\in[d]} = s^{1},s^{2}, \cdots,s^{d}$

### Setup

- Sample random values $s,\alpha$
- Calculate $g^{\alpha}$ and $g^{s^{i}}$, $g^{\alpha s^{i}}$
- Proving key ($g^{s^{i}},g^{\alpha s^{i}}$)
- Verification key: ($g^{\alpha}$ , $g^{t(s)}$ )

### Proving

- Assign coefficients $(c_{i})_{i \in 0,...,d}$ :

$$p(x)= c_{d}x^{d} +\cdots+ c_{1}x^{1}+c_{0}x^{0}$$

- Calculate $h(x)= \frac{p(x)}{t(x)}$
- Evaluate $g^{p(s)}$ and $g^{h(s)}$ using $g^{s^{i}}$
- Evaluate $g^{\alpha p(s)}$ using $g^{\alpha s^{i}}$
- Sample random $\delta$
- Set the randomized proof $\pi = (g^{\delta p(s)}, g^{\delta h(s)},g^{\delta
\alpha p(s)})$

### Verification

Check:

- Parse proof $\pi$ as $(g^{p},g^{h},g^{p'})$
- $e({g^{{p}'}},g)=e(g^{p},g^{\alpha})$
- $e(g^{p},g)=e(g^{t(s)},g^{h})$


>[!Conclusions]
>
>Prover can easily construct such polynomial $p(x)$ just by multiplying $t(x)$ by another bounded polynomial.
>
>Verifier knows that the prover has a valid polynomial but not which particular one.
