---
description: "The StatsGeometricCDF function returns the geometric cumulative distribution function."
slug: /commands/statsgeometriccdf
---

<div className="command-signature">

## <strong>StatsGeometricCDF</strong> (<em>x</em>, <em>p</em>) {#statsgeometriccdf}

</div>

The StatsGeometricCDF function returns the geometric cumulative distribution function

$$
\displaystyle F(x, p)=1-(1-p)^{x+1} .
$$

where *p* is the probability of success in a single trial and *x* is the number of trials for *x* >=0.

### *See Also* {#see-also}
[Statistical Analysis](/igorpro/analysis/statistics.md), [StatsGeometricPDF](/igorpro/commands/statsgeometricpdf.md), [StatsInvGeometricCDF](/igorpro/commands/statsinvgeometriccdf.md)