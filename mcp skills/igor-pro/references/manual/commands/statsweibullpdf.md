---
description: "The StatsWeibullPDF function returns the Weibull probability distribution function."
slug: /commands/statsweibullpdf
---

<div className="command-signature">

## <strong>StatsWeibullPDF</strong> (<em>x</em>, µ, σ, γ) {#statsweibullpdf}

</div>

The StatsWeibullPDF function returns the Weibull probability distribution function

$$
\displaystyle f(x ; \mu, \sigma, \gamma)=\frac{\gamma}{\sigma}\left(\frac{x-\mu}{\sigma}\right)^{\gamma-1} \exp \left[-\left(\frac{x-\mu}{\sigma}\right)^{\gamma}\right],
$$

with x>=*µ* and *σ*, γ>0. Here *µ* is the location parameter, *σ* is the scale parameter and γ is the shape parameter.

### *See Also* {#see-also}
[Statistical Analysis](/igorpro/analysis/statistics.md), [StatsWeibullCDF](/igorpro/commands/statsweibullcdf.md), [StatsInvWeibullCDF](/igorpro/commands/statsinvweibullcdf.md)