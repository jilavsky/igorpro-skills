---
description: "The expInt function returns the value of the exponential integral En (x)."
slug: /commands/expint
---

<div className="command-signature">

## <strong>expInt</strong> (<em>n</em>, <em>x</em>) {#expint}

</div>

The expInt function returns the value of the exponential integral *E*<sub>n </sub>(*x* ):

$$
\displaystyle E_{n}(x)=P \int_{1}^{\infty} \frac{e^{-x t}}{t^{n}} d t \quad(x>0 ; n=0,1,2 \ldots).
$$

### *See Also* {#see-also}
[ei](/igorpro/commands/ei.md), [ExpIntegralE1](/igorpro/commands/expintegrale1.md)

### *References* {#references}
Abramowitz, M., and I.A. Stegun, "Handbook of Mathematical Functions", 446 pp., Dover, New York, 1972.