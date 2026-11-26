---
description: "The Besseli function returns the modified Bessel function of the first kind, In (z), of ordern and argument z."
slug: /commands/besseli
---

<div className="command-signature">

## <strong>Besseli</strong> (<em>n</em>, <em>z</em>) {#besseli}

</div>

The Besseli function returns the modified Bessel function of the first kind, I<sub>n </sub>(*z* ), of order*n* and argument *z*. Supersedes the original [bessI](/igorpro/commands/bessi.md) function, which is supported for backwards compatibility only.

If *z* is real, a real value is returned, which means that if *z* is also negative, Besseli returns NaN unless n  is an integer.

For complex *z* a complex value is returned, and there are no restrictions on *z* except for possible overflow.

### *Details* {#details}
The calculation is performed using the SLATEC library. The function supports fractional and negative orders *n*, as well as real or complex arguments *z*.

### *See Also* {#see-also}
[Besselj](/igorpro/commands/besselj.md), [Besselk](/igorpro/commands/besselk.md), [Bessely](/igorpro/commands/bessely.md)