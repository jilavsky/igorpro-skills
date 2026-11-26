---
description: "The Bessely function returns the Bessel function of the second kind, Yn (z), of ordern and argument z."
slug: /commands/bessely
---

<div className="command-signature">

## <strong>Bessely</strong> (<em>n</em>, <em>z</em>) {#bessely}

</div>

The Bessely function returns the Bessel function of the second kind, Y<sub>n </sub>(*z* ), of order*n* and argument *z*. Supersedes the original [bessY](/igorpro/commands/bessy.md) function, which is supported for backwards compatibility only.

If *z* is real, a real value is returned, which means that if *z* is also negative, Bessely returns NaN unless n  is an integer.

For complex *z* a complex value is returned, and there are no restrictions on *z* except for possible overflow.

### *Details* {#details}
The calculation is performed using the SLATEC library. The function supports fractional and negative orders *n*, as well as real or complex arguments *z*.

### *See Also* {#see-also}
[Besseli](/igorpro/commands/besseli.md), [Besselj](/igorpro/commands/besselj.md), [Besselk](/igorpro/commands/besselk.md)