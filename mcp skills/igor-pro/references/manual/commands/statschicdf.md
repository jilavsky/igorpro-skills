---
description: "The StatsChiCDF function returns the chi-squared cumulative distribution function for the specified value and degrees of freedom n."
slug: /commands/statschicdf
---

<div className="command-signature">

## <strong>StatsChiCDF</strong> (<em>x</em>, <em>n</em>) {#statschicdf}

</div>

The StatsChiCDF function returns the chi-squared cumulative distribution function for the specified value and degrees of freedom n

$$
F(x ; n)=\frac{\displaystyle \gamma\left(\frac{n}{2}, \frac{x}{2}\right)}{\displaystyle \Gamma\left(\frac{n}{2}\right)} .
$$

where is *γ* (*a*,*b* ) the incomplete gamma function. The distribution can also be expressed as

$$
\displaystyle F(x ; n)=1-{gammq}\left(\frac{n}{2}, \frac{x}{2}\right) .
$$

### *See Also* {#see-also}
[Statistical Analysis](/igorpro/analysis/statistics.md), [StatsChiPDF](/igorpro/commands/statschipdf.md), [StatsInvChiCDF](/igorpro/commands/statsinvchicdf.md), [gammq](/igorpro/commands/gammq.md)