---
description: "The SinIntegral(z) function returns the sine integral of z. If z is real, a real value is returned. If z is complex then a complex value is returned."
slug: /commands/sinintegral
---

<div className="command-signature">

## <strong>SinIntegral</strong> (<em>z</em>) {#sinintegral}

</div>

The SinIntegral(*z*) function returns the sine integral of *z*.

If *z* is real, a real value is returned. If *z* is complex then a complex value is returned.

The SinIntegral function was added in Igor Pro 7.00.

### *Details* {#details}
The sin integral is defined by

$$
\displaystyle \operatorname{Si}(z)=\int_{0}^{z} \frac{\sin (t)}{t} d t .
$$

IGOR computes the SinIntegral using the expression:

$$
\displaystyle \operatorname{Si}(z)=z_{1} F_{2}\left(\frac{1}{2} ; \frac{3}{2}, \frac{3}{2} ;-\frac{z^{2}}{4}\right) .
$$

### *References* {#references}
Abramowitz, M., and I.A. Stegun, "Handbook of Mathematical Functions", Dover, New York, 1972. Chapter 5.

### *See Also* {#see-also}
[CosIntegral](/igorpro/commands/cosintegral.md), [ExpIntegralE1](/igorpro/commands/expintegrale1.md), [HyperGPFQ](/igorpro/commands/hypergpfq.md)