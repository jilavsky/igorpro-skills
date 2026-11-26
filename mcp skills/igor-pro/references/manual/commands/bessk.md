---
description: "Obsolete -- use Besselk. The bessK function returns the modified Bessel function of the second kind, Kn (x), of order n and argument x."
slug: /commands/bessk
---

<div className="command-signature">

## <strong>bessK</strong> (<em>n</em>,<em>x</em> [, <em>algorithm</em>  [, <em>accuracy</em> ]]) {#bessk}

</div>

:::warning
Obsolete -- use [Besselk](/igorpro/commands/besselk.md).
:::

The bessK function returns the modified Bessel function of the second kind, K<sub>n </sub>(*x*), of order *n* and argument *x*.

For real x, the optional parameter *algorithm* selects between a faster, less accurate calculation method and slower, more accurate methods. In addition, when *algorithm* is zero or absent, the order *n* is truncated to an integer.

When *algorithm* is included and is 1, *accuracy* can be used to specify the desired fractional accuracy. See below for details about algorithms.

If *x* is complex, a complex result is returned. In this case, *algorithm* and *accuracy* are ignored. The order *n* can be fractional, and must be real.

### *Details* {#details}
See the [bessI](/igorpro/commands/bessi.md) function for details on algorithms, accuracy and speed of execution.

When *algorithm* is 1, pairs of values for bessJ and bessY are calculated simultaneously. The values are stored, and a subsequent call to bessJ after a call to bessK (or vice-versa) with the same *n*, *x*, and *accuracy* will be very fast.