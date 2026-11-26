---
description: "The StatsInvGeometricCDF function returns the inverse of the geometric cumulative distribution function."
slug: /commands/statsinvgeometriccdf
---

<div className="command-signature">

## <strong>StatsInvGeometricCDF</strong> (<em>cdf</em>, <em>p</em>) {#statsinvgeometriccdf}

</div>

The StatsInvGeometricCDF function returns the inverse of the geometric cumulative distribution function

$$
\displaystyle x=\frac{\ln (1-c d f)}{\ln (1-p)}-1.
$$

where *p* is the probability of success in a single trial and *x* is the number of trials.

### *See Also* {#see-also}
[Statistical Analysis](/igorpro/analysis/statistics.md), [StatsGeometricPDF](/igorpro/commands/statsgeometricpdf.md), [StatsGeometricCDF](/igorpro/commands/statsgeometriccdf.md)