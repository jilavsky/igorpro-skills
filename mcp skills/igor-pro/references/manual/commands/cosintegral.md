---
description: "The CosIntegral(z) function returns the cosine integral of z. If z is real, a real value is returned. If z is complex then a complex value is returned."
slug: /commands/cosintegral
---

<div className="command-signature">

## <strong>CosIntegral</strong> (<em>z</em>) {#cosintegral}

</div>

The CosIntegral(*z*) function returns the cosine integral of *z*.

If *z* is real, a real value is returned. If *z* is complex then a complex value is returned.

The CosIntegral function was added in Igor Pro 7.00.

### *Details* {#details}
The cosine integral is defined by

$$
\displaystyle \operatorname{Ci}(z)=\gamma+\ln (z)+\int_{0}^{z} \frac{\cos (t)-1}{t} d t, \quad(|\arg (z)|<\pi)
$$

where γ is the Euler-Mascheroni constant 0.5772156649015328606065.

IGOR computes the cosine integral using the expression:

$$
\displaystyle \operatorname{Ci}(z)=-\frac{Z^{2}}{4}{ }_{2} F_{3}\left(1,1 ; 2,2, \frac{3}{2} ;-\frac{z^{2}}{4}\right)+\ln (z)+\gamma,
$$

### *References* {#references}
Abramowitz, M., and I.A. Stegun, "Handbook of Mathematical Functions", Dover, New York, 1972. Chapter 5.

### *See Also* {#see-also}
[SinIntegral](/igorpro/commands/sinintegral.md), [ExpIntegralE1](/igorpro/commands/expintegrale1.md), [HyperGPFQ](/igorpro/commands/hypergpfq.md)