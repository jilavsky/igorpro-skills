---
description: "The StatsNormalCDF function returns the normal cumulative distribution function."
slug: /commands/statsnormalcdf
---

<div className="command-signature">

## <strong>StatsNormalCDF</strong> (<em>x</em>, µ, σ) {#statsnormalcdf}

</div>

The StatsNormalCDF function returns the normal cumulative distribution function.

$$
\displaystyle F(x, \mu, \sigma)=\frac{1}{2}+\frac{1}{2} \operatorname{erf}\left(\frac{x-\mu}{\sigma \sqrt{2}}\right),
$$

where *erf* is the error function.

### *See Also* {#see-also}
[Statistical Analysis](/igorpro/analysis/statistics.md), [StatsNormalPDF](/igorpro/commands/statsnormalpdf.md), [StatsInvNormalCDF](/igorpro/commands/statsinvnormalcdf.md)