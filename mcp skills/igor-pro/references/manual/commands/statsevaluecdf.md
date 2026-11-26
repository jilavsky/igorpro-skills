---
description: "The StatsEValueCDF function returns the extreme-value (type I, Gumbel) cumulative distribution function."
slug: /commands/statsevaluecdf
---

<div className="command-signature">

## <strong>StatsEValueCDF</strong> (<em>x</em>, µ, σ) {#statsevaluecdf}

</div>

The StatsEValueCDF function returns the extreme-value (type I, Gumbel) cumulative distribution function

$$
\displaystyle F(x ; \mu, \sigma)=1-\exp \left(-\exp \left(\frac{x-\mu}{\sigma}\right)\right),
$$

where σ > 0. This is also known as the "minimum" form or distribution of the smallest extreme. To obtain the distribution of the largest extreme reverse the sign of *σ*.

### *See Also* {#see-also}
[Statistical Analysis](/igorpro/analysis/statistics.md), [StatsEValuePDF](/igorpro/commands/statsevaluepdf.md), [StatsInvEValueCDF](/igorpro/commands/statsinvevaluecdf.md), [StatsGEVCDF](/igorpro/commands/statsgevcdf.md), [StatsGEVPDF](/igorpro/commands/statsgevpdf.md)