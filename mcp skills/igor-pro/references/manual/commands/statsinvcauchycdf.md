---
description: "The StatsInvCauchyCDF function returns the inverse of the Cauchy-Lorentz cumulative distribution function."
slug: /commands/statsinvcauchycdf
---

<div className="command-signature">

## <strong>StatsInvCauchyCDF</strong> (<em>cdf</em>, µ, σ) {#statsinvcauchycdf}

</div>

The StatsInvCauchyCDF function returns the inverse of the Cauchy-Lorentz cumulative distribution function

$$
\displaystyle x=\mu+\sigma \tan \left[\pi\left(c d f-\frac{1}{2}\right)\right] .
$$

It returns NaN for *cdf* <0 or *cdf* > 1.

### *See Also* {#see-also}
[Statistical Analysis](/igorpro/analysis/statistics.md), [StatsCauchyPDF](/igorpro/commands/statscauchypdf.md), [StatsCauchyCDF](/igorpro/commands/statscauchycdf.md)