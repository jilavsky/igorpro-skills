---
description: "The StatsNCChiCDF function returns the noncentral chi-squared cumulative distribution function."
slug: /commands/statsncchicdf
---

<div className="command-signature">

## <strong>StatsNCChiCDF</strong> (<em>x</em>, <em>n</em>, <em>d</em>) {#statsncchicdf}

</div>

The StatsNCChiCDF function returns the noncentral chi-squared cumulative distribution function.

$$
\displaystyle F(x ; n, d)=\sum_{i=1}^{\infty} \exp (d / 2) \frac{(d / 2)^{i}}{i!} F_{c}(x ; n+2 i),
$$

where *n* >0 corresponds to degrees of freedom, *d* >=0 is the noncentrality parameter, and *F*<sub>c</sub>  is the central chi-squared distribution.

### *References* {#references}
Abramowitz, M., and I.A. Stegun, "Handbook of Mathematical Functions", 446 pp., Dover, New York, 1972.

### *See Also* {#see-also}
[Statistical Analysis](/igorpro/analysis/statistics.md), [StatsChiPDF](/igorpro/commands/statschipdf.md), [StatsNCChiPDF](/igorpro/commands/statsncchipdf.md), [StatsChiCDF](/igorpro/commands/statschicdf.md)