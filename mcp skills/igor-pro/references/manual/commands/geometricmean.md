---
description: "The GeometricMean function returns the arithmetic-geometric mean of two positive real numbers a and b."
slug: /commands/geometricmean
---

<div className="command-signature">

## <strong>GeometricMean</strong> (<em>a</em>, <em>b</em>) {#geometricmean}

</div>

The GeometricMean function returns the arithmetic-geometric mean of two positive real numbers *a* and *b*. The mean is computed by creating two sequences {a<sub>i</sub>} and {b<sub>i</sub>} initialized to the input values: a<sub>0</sub>=a and b<sub>0</sub>=b with

$$
\displaystyle a_{n+1}=\frac{1}{2}\left(a_{n}+b_{n}\right),
$$

$$
\displaystyle b_{n+1}=\sqrt{a_{n} b_{n}} .
$$

The two sequences converge in a few iterations to a single value which is the arithmetic-geometric mean.

### *See Also* {#see-also}
[EllipticK](/igorpro/commands/elliptick.md), [EllipticE](/igorpro/commands/elliptice.md)