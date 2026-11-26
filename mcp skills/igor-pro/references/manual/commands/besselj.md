---
description: "The Besselj function returns the Bessel function of the first kind, Jn (z), of ordern and argument z."
slug: /commands/besselj
---

<div className="command-signature">

## <strong>Besselj</strong> (<em>n</em>, <em>z</em>) {#besselj}

</div>

The Besselj function returns the Bessel function of the first kind, J<sub>n </sub>(*z* ), of order*n* and argument *z*. Supersedes the original [bessJ](/igorpro/commands/bessj.md) function, which is supported for backwards compatibility only.

If *z* is real, a real value is returned, which means that if *z* is also negative, Besselj returns NaN unless n  is an integer.

For complex *z* a complex value is returned, and there are no restrictions on *z* except for possible overflow.

### *Details* {#details}
The calculation is performed using the SLATEC library. The function supports fractional and negative orders *n*, as well as real or complex arguments *z*.

### *See Also* {#see-also}
[Besseli](/igorpro/commands/besseli.md), [Besselk](/igorpro/commands/besselk.md), [Bessely](/igorpro/commands/bessely.md)