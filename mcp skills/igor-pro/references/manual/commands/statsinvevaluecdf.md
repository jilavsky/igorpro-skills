---
description: "The StatsInvEValueCDF function returns the inverse of the extreme-value (type I, Gumbel) cumulative distribution function."
slug: /commands/statsinvevaluecdf
---

<div className="command-signature">

## <strong>StatsInvEValueCDF</strong> (<em>cdf</em>, µ, σ) {#statsinvevaluecdf}

</div>

The StatsInvEValueCDF function returns the inverse of the extreme-value (type I, Gumbel) cumulative distribution function

$$
\displaystyle x=\mu+\sigma \ln [-\ln (1-c d f)],
$$

wher σ>0.  It returns NaN when *cdf* <0 or when *cdf* >1. This inverse applies to the "minimum" form of the distribution. Reverse the sign of σ to obtain the inverse distribution of the maximum form.

### *See Also* {#see-also}
[Statistical Analysis](/igorpro/analysis/statistics.md), [StatsEValuePDF](/igorpro/commands/statsevaluepdf.md), [StatsEValueCDF](/igorpro/commands/statsevaluecdf.md), [StatsGEVCDF](/igorpro/commands/statsgevcdf.md), [StatsGEVPDF](/igorpro/commands/statsgevpdf.md)