---
description: "The StatsRayleighCDF function returns the Rayleigh cumulative distribution function."
slug: /commands/statsrayleighcdf
---

<div className="command-signature">

## <strong>StatsRayleighCDF</strong> (<em>x</em> [, σ [, µ ]]) {#statsrayleighcdf}

</div>

The StatsRayleighCDF function returns the Rayleigh cumulative distribution function.

$$
\displaystyle F(x ; \sigma, \mu)=1-\exp \left(-\frac{(x-\mu)^{2}}{2 \sigma^{2}}\right),
$$

with defaults σ=1 and *µ*=0. It returns NaN for σ<=0 and zero for x<=*µ*.

### *See Also* {#see-also}
[Statistical Analysis](/igorpro/analysis/statistics.md), [StatsRayleighPDF](/igorpro/commands/statsrayleighpdf.md), [StatsInvRayleighCDF](/igorpro/commands/statsinvrayleighcdf.md)