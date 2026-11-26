---
description: "Returns the inverse of the Rayleigh cumulative distribution function (CDF) given by."
slug: /commands/statsinvrayleighcdf
---

<div className="command-signature">

## <strong>StatsInvRayleighCDF</strong> (<em>cdf</em>  [, σ [, µ ]]) {#statsinvrayleighcdf}

</div>

Returns the inverse  of the Rayleigh cumulative distribution function (CDF) given by

$$
\displaystyle x=\mu+\sigma \sqrt{-2 \ln (1-c d f)},
$$

with defaults σ=1 and *µ*=0. It returns NaN for σ<=0 and zero for x<=*µ*.

### *See Also* {#see-also}
[Statistical Analysis](/igorpro/analysis/statistics.md), [StatsRayleighPDF](/igorpro/commands/statsrayleighpdf.md), [StatsRayleighCDF](/igorpro/commands/statsrayleighcdf.md)