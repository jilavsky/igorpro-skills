---
description: "The StatsVonMisesPDF function returns the von Mises probability distribution function."
slug: /commands/statsvonmisespdf
---

<div className="command-signature">

## <strong>StatsVonMisesPDF</strong> (θ, <em>a</em>, <em>b</em>) {#statsvonmisespdf}

</div>

The StatsVonMisesPDF function returns the von Mises probability distribution function

$$
\displaystyle f(\theta ; a, b)=\frac{\exp (b \cos (\theta-a))}{2 \pi I_{0}(b)} .
$$

where *I*<sub>0</sub>(*b* ) is the modified Bessel function of the first kind [bessI](/igorpro/commands/bessi.md), and 0<θ<=2π, 0<*a* <=2π, and *b* >0.

### *References* {#references}
Evans, M., N. Hastings, and B. Peacock, *Statistical Distributions*, 3rd ed., Wiley, New York, 2000.

### *See Also* {#see-also}
[Statistical Analysis](/igorpro/analysis/statistics.md), [StatsVonMisesCDF](/igorpro/commands/statsvonmisescdf.md), [StatsInvVonMisesCDF](/igorpro/commands/statsinvvonmisescdf.md), [StatsVonMisesNoise](/igorpro/commands/statsvonmisesnoise.md)