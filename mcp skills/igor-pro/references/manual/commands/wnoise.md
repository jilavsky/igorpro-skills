---
description: "The wnoise function returns a pseudo-random value from the two-parameter Weibull distribution characterized by the shape and scale, the respective gamma and…"
slug: /commands/wnoise
---

<div className="command-signature">

## <strong>wnoise</strong> (<em>shape</em>, <em>scale</em>) {#wnoise}

</div>

The wnoise function returns a pseudo-random value from the two-parameter Weibull distribution characterized by the *shape* and *scale*, the respective *gamma* and *alpha* parameters. The two-parameter Weibull probability distribution function is

$$
\displaystyle f(x ; \alpha, \gamma)=\frac{\gamma}{\alpha} x^{\gamma-1} \exp \left[-\frac{1}{\alpha} x^{\gamma}\right] \quad \begin{array}{l}
x \geq 0 \\
\alpha>0 \\
\gamma>0
\end{array}
$$

The mean of the Weibull distribution is

$$
\displaystyle \alpha^{\frac{1}{\gamma}} \Gamma\left(1+\frac{1}{\gamma}\right),
$$

and the variance is

$$
\displaystyle \alpha^{\frac{2}{\gamma}} \Gamma\left(1+\frac{2}{\gamma}\right)-\alpha^{\frac{2}{\gamma}}\left[\Gamma\left(1+\frac{1}{\gamma}\right)\right]^{2} .
$$

Note that this definition of the PDF uses different scaling than the one used in StatsWeibullPDF. To match the scaling of StatsWeibullPDF multiply the result from Wnoise by the factor scale^(1-1/shape).

The random number generator initializes using the system clock when Igor Pro starts. This almost guarantees that you will never repeat a sequence. For repeatable "random" numbers, use [SetRandomSeed](/igorpro/commands/setrandomseed.md). The algorithm uses the Mersenne Twister random number generator.

### *See Also* {#see-also}
[SetRandomSeed](/igorpro/commands/setrandomseed.md), [Noise Functions](/igorpro/analysis/statistics.md#noise-functions), [Statistical Analysis](/igorpro/analysis/statistics.md)