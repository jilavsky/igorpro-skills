---
description: "The Besselk function returns the modified Bessel function of the second kind, Kn (z), of ordern and argument z."
slug: /commands/besselk
---

<div className="command-signature">

## <strong>Besselk</strong> (<em>n</em>, <em>z</em>) {#besselk}

</div>

The Besselk function returns the modified Bessel function of the second kind, K<sub>n </sub><sub>(</sub>*z*), of order*n* and argument *z*. Supersedes the original [bessK](/igorpro/commands/bessk.md) function, which is supported for backwards compatibility only.

If *z* is real, a real value is returned, which means that if *z* is also negative, Besselk returns NaN unless n  is an integer.

For complex *z* a complex value is returned, and there are no restrictions on *z* except for possible overflow.

### *Details* {#details}
The calculation is performed using the SLATEC library. The function supports fractional orders *n*, as well as real or complex arguments *z*.

### *See Also* {#see-also}
[Besseli](/igorpro/commands/besseli.md), [Besselj](/igorpro/commands/besselj.md), [Bessely](/igorpro/commands/bessely.md)