---
description: "The hyperGPFQ function returns the generalized hypergeometric function."
slug: /commands/hypergpfq
---

<div className="command-signature">

## <strong>hyperGPFQ</strong> (<em>waveA</em>, <em>waveB</em>, <em>z</em>) {#hypergpfq}

</div>

The hyperGPFQ function returns the generalized hypergeometric function

$$
\displaystyle { }_{p} F_{q}\left(\left\{a_{1}, \ldots a_{p}\right\},\left\{b_{1}, \ldots b_{q}\right\} ; z\right)=\sum_{n=0}^{\infty} \frac{\left(a_{1}\right)_{n}\left(a_{2}\right)_{n} \ldots\left(a_{p}\right)_{n} z^{n}}{\left(b_{1}\right)_{n}\left(b_{2}\right)_{n} \ldots\left(b_{q}\right)_{n} n!},
$$

where (a)<sub>n </sub>is the Pochhammer symbol

$$
\displaystyle (a)_{n}=a(a+1) \ldots(a+n-1) .
$$

**Note**: The series evaluation may be computationally intensive. You can abort the computation by pressing the [User Abort Key Combinations](/igorpro/programming/programming.md#user-abort-key-combinations).

### *See Also* {#see-also}
[hyperG0F1](/igorpro/commands/hyperg0f1.md), [hyperG1F1](/igorpro/commands/hyperg1f1.md), [hyperG2F1](/igorpro/commands/hyperg2f1.md), [CosIntegral](/igorpro/commands/cosintegral.md), [ExpIntegralE1](/igorpro/commands/expintegrale1.md), [SinIntegral](/igorpro/commands/sinintegral.md)

### *References* {#references}
The PFQ algorithm was developed by Warren F. Perger, Atul Bhalla and Mark Nardin.