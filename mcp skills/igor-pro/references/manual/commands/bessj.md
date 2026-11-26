---
description: "Obsolete -- use Besselj. The bessJ function returns the Bessel function of the first kind, Jn (x), of order n and argument x."
slug: /commands/bessj
---

<div className="command-signature">

## <strong>bessJ</strong> (<em>n</em>,<em>x</em> [, <em>algorithm</em>  [, <em>accuracy</em> ]]) {#bessj}

</div>

:::warning
Obsolete -- use [Besselj](/igorpro/commands/besselj.md).
:::

The bessJ function returns the Bessel function of the first kind, J<sub>n </sub>(*x* ), of order *n* and argument *x*.

For real x, the optional parameter *algorithm* selects between a faster, less accurate calculation method and slower, more accurate methods. In addition, when *algorithm* is zero or absent, the order *n* is truncated to an integer.

When *algorithm* is included and is 1, *accuracy* can be used to specify the desired fractional accuracy. See below for details about algorithms.

if *x* is complex, a complex result is returned. In this case, *algorithm* and *accuracy* are ignored. The order *n* can be fractional, and must be real.

### *Details* {#details}
See the [bessI](/igorpro/commands/bessi.md) function for details on algorithms, accuracy and speed of execution.

When *algorithm* is 1, pairs of values for bessJ and bessY are calculated simultaneously. The values are stored, and a subsequent call to bessY after a call to bessJ (or vice-versa) with the same *n*, *x*, and *accuracy* will be very fast.