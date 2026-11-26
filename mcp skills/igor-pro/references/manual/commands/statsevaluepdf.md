---
description: "The StatsEValuePDF function returns the extreme-value (type I, Gumbel) probability distribution function."
slug: /commands/statsevaluepdf
---

<div className="command-signature">

## <strong>StatsEValuePDF</strong> (<em>x</em>, µ, σ) {#statsevaluepdf}

</div>

The StatsEValuePDF function returns the extreme-value (type I, Gumbel) probability distribution function

$$
\displaystyle f(x ; \mu, \sigma)=\frac{1}{\sigma} \exp \left(\frac{x-\mu}{\sigma}\right) \exp \left(-\exp \left(\frac{x-\mu}{\sigma}\right)\right),
$$

where σ > 0. This is also known as the "minimum" form or distribution of the smallest extreme. To obtain the distribution of the largest extreme reverse the sign of *σ*.

### *See Also* {#see-also}
[Statistical Analysis](/igorpro/analysis/statistics.md), [StatsEValueCDF](/igorpro/commands/statsevaluecdf.md), [StatsInvEValueCDF](/igorpro/commands/statsinvevaluecdf.md), [StatsGEVCDF](/igorpro/commands/statsgevcdf.md), [StatsGEVPDF](/igorpro/commands/statsgevpdf.md)