---
description: "The sphericalBessJ function returns the spherical Bessel function of the first kind and order n."
slug: /commands/sphericalbessj
---

<div className="command-signature">

## <strong>sphericalBessJ</strong> (<em>n</em>, <em>x</em> [, <em>accuracy</em>]) {#sphericalbessj}

</div>

The sphericalBessJ function returns the spherical Bessel function of the first kind and order *n*.

$$
\displaystyle j_{n}(x)=\sqrt{\frac{\pi}{2 x}} J_{n+1 / 2}(x) .
$$

For example:

$$
\begin{array}{l}
\displaystyle j_{0}(x)=\frac{\sin (x)}{x} \\
\\
\displaystyle j_{1}(x)=\frac{\sin (x)}{x^{2}}-\frac{\cos (x)}{x} \\
\\
\displaystyle j_{2}(x)=\left(\frac{3}{x^{3}}-\frac{1}{x}\right) \sin (x)-\frac{3}{x^{2}} \cos (x) .
\end{array}
$$

### *Details* {#details}
See the [bessI](/igorpro/commands/bessi.md) function for details on accuracy and speed of execution.

### *See Also* {#see-also}
[sphericalBessJD](/igorpro/commands/sphericalbessjd.md), [sphericalBessY](/igorpro/commands/sphericalbessy.md)

### *References* {#references}
Abramowitz, M., and I.A. Stegun, "Handbook of Mathematical Functions", 446 pp., Dover, New York, 1972.