---
description: "The gammaInc function returns the value of the incomplete gamma function, defined by the integral."
slug: /commands/gammainc
---

<div className="command-signature">

## <strong>gammaInc</strong> (<em>a</em>, <em>x</em> [, <em>upperTail</em> ]) {#gammainc}

</div>

The gammaInc function returns the value of the incomplete gamma function, defined by the integral

$$
\displaystyle \Gamma(a, x)=\int_{x}^{\infty} e^{-t} t^{a-1} d t.
$$

If *upperTail* is zero, the limits of integration are 0 to x. If *upperTail* is absent, it defaults to 1, and the limits of integration are x to infinity, as shown. Note that gammaInc(a, x) = gamma(a) - gammaInc(a, x, 0).

Defined for x > 0, a >= 0 (*upperTail* = zero or absent) or a > 0 (*upperTail* = 0).

### *See Also* {#see-also}
[gamma](/igorpro/commands/gamma.md), [gammp](/igorpro/commands/gammp.md), [gammq](/igorpro/commands/gammq.md)