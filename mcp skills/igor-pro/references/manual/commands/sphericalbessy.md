---
description: "The sphericalBessY function returns the spherical Bessel function of the second kind and order n."
slug: /commands/sphericalbessy
---

<div className="command-signature">

## <strong>sphericalBessY</strong> (<em>n</em>, <em>x</em> [, <em>accuracy</em>]) {#sphericalbessy}

</div>

The sphericalBessY function returns the spherical Bessel function of the second kind and order *n*.

$$
\displaystyle y_{n}(x)=\sqrt{\frac{\pi}{2 x}} Y_{n+1 / 2}(x) .
$$

$$
\begin{array}{l}
\displaystyle y_{0}(x)=-\frac{\cos (x)}{x} \\
\\
\displaystyle y_{1}(x)=-\frac{\cos (x)}{x^{2}}-\frac{\sin (x)}{x} \\
\\
\displaystyle y_{2}(x)=\left(\frac{1}{x}-\frac{3}{x^{3}}\right) \cos (x)-\frac{3}{x^{2}} \sin (x) .
\end{array}
$$

### *Details* {#details}
See the [bessI](/igorpro/commands/bessi.md) function for details on accuracy and speed of execution.

### *See Also* {#see-also}
[sphericalBessYD](/igorpro/commands/sphericalbessyd.md), [sphericalBessJ](/igorpro/commands/sphericalbessj.md)

### *References* {#references}
Abramowitz, M., and I.A. Stegun, "Handbook of Mathematical Functions", 446 pp., Dover, New York, 1972.