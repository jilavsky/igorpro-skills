---
description: "The hyperG2F1 function returns the confluent hypergeometric function $$ \\displaystyle { }_{2} F_{1}(a, b, c; z)=\\sum_{n=0}^{\\infty} \\frac{(a)_{n}(b)_{n}…"
slug: /commands/hyperg2f1
---

<div className="command-signature">

## <strong>hyperG2F1</strong> (<em>a</em>, <em>b</em>, <em>c</em>, <em>z</em>) {#hyperg2f1}

</div>

The hyperG2F1 function returns the confluent hypergeometric function

$$
\displaystyle { }_{2} F_{1}(a, b, c ; z)=\sum_{n=0}^{\infty} \frac{(a)_{n}(b)_{n} z^{n}}{(c)_{n} n!},
$$

where (a)<sub>n</sub>is the Pochhammer symbol

$$
\displaystyle (a)_{n}=a(a+1) \ldots(a+n-1) .
$$

**Note**: The series evaluation may be computationally intensive. You can abort the computation by pressing the [User Abort Key Combinations](/igorpro/programming/programming.md#user-abort-key-combinations).

### *See Also* {#see-also}
[hyperG0F1](/igorpro/commands/hyperg0f1.md), [hyperG1F1](/igorpro/commands/hyperg1f1.md), [hyperGPFQ](/igorpro/commands/hypergpfq.md)

### *References* {#references}
The PFQ algorithm was developed by Warren F. Perger, Atul Bhalla and Mark Nardin.