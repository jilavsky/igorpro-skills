---
description: "The StatsWeibullCDF function returns the Weibull cumulative distribution function."
slug: /commands/statsweibullcdf
---

<div className="command-signature">

## <strong>StatsWeibullCDF</strong> (<em>x</em>, µ, σ, γ) {#statsweibullcdf}

</div>

The StatsWeibullCDF function returns the Weibull cumulative distribution function

$$
\displaystyle F(x ; \mu, \sigma, \gamma)=1-\exp \left[-\left(\frac{x-\mu}{\sigma}\right)^{\gamma}\right], \quad \quad x \geq \mu \text { and } \sigma, \gamma>0 .
$$

### *See Also* {#see-also}
[Statistical Analysis](/igorpro/analysis/statistics.md), [StatsWeibullPDF](/igorpro/commands/statsweibullpdf.md), [StatsInvWeibullCDF](/igorpro/commands/statsinvweibullcdf.md)