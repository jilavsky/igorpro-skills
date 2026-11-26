---
description: "The StatsInvExpCDF function returns the inverse of the exponential cumulative distribution function."
slug: /commands/statsinvexpcdf
---

<div className="command-signature">

## <strong>StatsInvExpCDF</strong> (<em>cdf</em>, µ, σ) {#statsinvexpcdf}

</div>

The StatsInvExpCDF function returns the inverse of the exponential cumulative distribution function

$$
\displaystyle x=\mu-\sigma \ln (1-c d f).
$$

It returns NaN for *cdf* <0 or *cdf* > 1.

### *See Also* {#see-also}
[Statistical Analysis](/igorpro/analysis/statistics.md), [StatsExpPDF](/igorpro/commands/statsexppdf.md), [StatsExpCDF](/igorpro/commands/statsexpcdf.md)