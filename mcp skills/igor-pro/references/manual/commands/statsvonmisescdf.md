---
description: "The StatsVonMisesCDF function returns the von Mises cumulative distribution function."
slug: /commands/statsvonmisescdf
---

<div className="command-signature">

## <strong>StatsVonMisesCDF</strong> (<em>x</em>, <em>a</em>, <em>b</em>) {#statsvonmisescdf}

</div>

The StatsVonMisesCDF function returns the von Mises cumulative distribution function

$$
\displaystyle F(\theta ; a, b)=\frac{1}{2 \pi I_{0}(b)} \int_{0}^{\theta} \exp (b \cos (x-a)) d x.
$$

where *I*<sub>0</sub>(*b* ) is the modified Bessel function of the first kind [bessI](/igorpro/commands/bessi.md), and 0<θ<=2π, 0<*a* <=2π, and *b* >0.

### *References* {#references}
Evans, M., N. Hastings, and B. Peacock, *Statistical Distributions*, 3rd ed., Wiley, New York, 2000.

### *See Also* {#see-also}
[Statistical Analysis](/igorpro/analysis/statistics.md), [StatsVonMisesPDF](/igorpro/commands/statsvonmisespdf.md), [StatsInvVonMisesCDF](/igorpro/commands/statsinvvonmisescdf.md), [StatsVonMisesNoise](/igorpro/commands/statsvonmisesnoise.md)