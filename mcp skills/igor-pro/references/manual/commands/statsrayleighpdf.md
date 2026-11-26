---
description: "The StatsRayleighPDF function returns the Rayleigh probability distribution function."
slug: /commands/statsrayleighpdf
---

<div className="command-signature">

## <strong>StatsRayleighPDF</strong> (<em>x</em> [, σ  [, µ ]]) {#statsrayleighpdf}

</div>

The StatsRayleighPDF function returns the Rayleigh probability distribution function.

$$
\displaystyle f(x ; \sigma, \mu)=\frac{x-\mu}{\sigma^{2}} \exp \left(-\frac{(x-\mu)^{2}}{2 \sigma^{2}}\right),
$$

with defaults σ=1 and *µ*=0. It returns NaN for σ<=0 and zero for x<=*µ*.

### *See Also* {#see-also}
[Statistical Analysis](/igorpro/analysis/statistics.md), [StatsRayleighCDF](/igorpro/commands/statsrayleighcdf.md), [StatsInvRayleighCDF](/igorpro/commands/statsinvrayleighcdf.md)