---
description: "The StatsExpCDF function returns the exponential cumulative distribution function."
slug: /commands/statsexpcdf
---

<div className="command-signature">

## <strong>StatsExpCDF</strong> (<em>x</em>, µ, σ) {#statsexpcdf}

</div>

The StatsExpCDF function returns the exponential cumulative distribution function

$$
\displaystyle F(x ; \mu, \sigma)=1-\exp \left(-\frac{x-\mu}{\sigma}\right),
$$

where *x* >= *µ* and σ > 0. It returns NaN for σ = 0.

### *See Also* {#see-also}
[Statistical Analysis](/igorpro/analysis/statistics.md), [StatsExpPDF](/igorpro/commands/statsexppdf.md), [StatsInvExpCDF](/igorpro/commands/statsinvexpcdf.md)