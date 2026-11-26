---
description: "The ExpIntegralE1(z) function returns the exponential integral of z. If z is real, a real value is returned. If z is complex then a complex value is returned."
slug: /commands/expintegrale1
---

<div className="command-signature">

## <strong>ExpIntegralE1</strong> (<em>z</em>) {#expintegrale1}

</div>

The ExpIntegralE1(*z*) function returns the exponential integral of *z*.

If *z* is real, a real value is returned. If *z* is complex then a complex value is returned.

The ExpIntegralE1 function was added in Igor Pro 7.00.

### *Details* {#details}
The exponential integral is defined by

$$
\displaystyle E_{1}(z)=\int_{z}^{\infty} \frac{e^{-t}}{t} d t, \quad(|\arg (z)|<\pi).
$$

### *References* {#references}
Abramowitz, M., and I.A. Stegun, "Handbook of Mathematical Functions", Dover, New York, 1972. Chapter 5.

### *See Also* {#see-also}
[ExpInt](/igorpro/commands/expint.md), [CosIntegral](/igorpro/commands/cosintegral.md), [SinIntegral](/igorpro/commands/sinintegral.md), [HyperGPFQ](/igorpro/commands/hypergpfq.md)