---
description: "The StatsCauchyPDF function returns the Cauchy-Lorentz probability distribution function."
slug: /commands/statscauchypdf
---

<div className="command-signature">

## <strong>StatsCauchyPDF</strong> (<em>x</em>, µ, σ) {#statscauchypdf}

</div>

The StatsCauchyPDF function returns the Cauchy-Lorentz probability distribution function

$$
f(x ; \mu, \sigma)=\frac{1}{\sigma \pi} \frac{1}{\displaystyle 1+\left(\frac{x-\mu}{\sigma}\right)^{2}},
$$

where *µ* is the location parameter and σ is the scale parameter. Use *µ*=0 and *σ*=1 for the standard form of the Cauchy-Lorentz distribution.

### *See Also* {#see-also}
[Statistical Analysis](/igorpro/analysis/statistics.md), [StatsCauchyCDF](/igorpro/commands/statscauchycdf.md), [StatsInvCauchyCDF](/igorpro/commands/statsinvcauchycdf.md)