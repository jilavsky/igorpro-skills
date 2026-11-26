---
description: "The StatsVonMisesNoise function returns a pseudo-random number from a von Mises distribution whose probability density is."
slug: /commands/statsvonmisesnoise
---

<div className="command-signature">

## <strong>StatsVonMisesNoise</strong> (<em>a</em>, <em>b</em>) {#statsvonmisesnoise}

</div>

The StatsVonMisesNoise function returns a pseudo-random number from a von Mises distribution whose probability density is

$$
\displaystyle f(\theta ; a, b)=\frac{\exp [b \cos (\theta-a)]}{2 \pi I_{0}(b)},
$$

where *I*<sub>0</sub> is the zeroth order modified Bessel function of the first kind ([bessI](/igorpro/commands/bessi.md)) and 0 < θ <= 2π, 0 < a <= 2π and b > 0.

### *References* {#references}
Best, D.J., and N. I. Fisher, Efficient simulation of von Mises distribution, *Appl. Statist.*, *28*, 152-157, 1979.

### *See Also* {#see-also}
[StatsVonMisesPDF](/igorpro/commands/statsvonmisespdf.md), [StatsVonMisesCDF](/igorpro/commands/statsvonmisescdf.md), [StatsInvVonMisesCDF](/igorpro/commands/statsinvvonmisescdf.md)

[Statistical Analysis](/igorpro/analysis/statistics.md), [Noise Functions](/igorpro/analysis/statistics.md#noise-functions)