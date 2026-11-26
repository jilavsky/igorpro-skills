---
description: "The hyperG0F1 function returns the confluent hypergeometric limit function."
slug: /commands/hyperg0f1
---

<div className="command-signature">

## <strong>hyperG0F1</strong> (<em>b</em>, <em>z</em>) {#hyperg0f1}

</div>

The hyperG0F1 function returns the confluent hypergeometric limit function

$$
\displaystyle { }_{0} F_{1}(b ; z)=\sum_{i=0}^{\infty} \frac{z^{i}}{i!(b)_{i}},
$$

where 
$$
\displaystyle (b)_{i}
$$
 is the Pochhammer symbol

$$
\displaystyle (b)_{i}=b(b+1) \ldots(b+i-1) .
$$

The series evaluation may be computationally intensive. You can abort the computation by pressing the [User Abort Key Combinations](/igorpro/programming/programming.md#user-abort-key-combinations).

### *See Also* {#see-also}
[hyperG1F1](/igorpro/commands/hyperg1f1.md), [hyperG2F1](/igorpro/commands/hyperg2f1.md), [hyperGPFQ](/igorpro/commands/hypergpfq.md)

### *References* {#references}
The PFQ algorithm was developed by Warren F. Perger, Atul Bhalla and Mark Nardin.