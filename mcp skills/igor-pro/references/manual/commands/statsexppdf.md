---
description: "The StatsExpPDF function returns the exponential probability distribution function."
slug: /commands/statsexppdf
---

<div className="command-signature">

## <strong>StatsExpPDF</strong> (<em>x</em>, µ, σ) {#statsexppdf}

</div>

The StatsExpPDF function returns the exponential probability distribution function

$$
\displaystyle f(x ; \mu, \sigma)=\frac{1}{\sigma} \exp \left(-\frac{x-\mu}{\sigma}\right),
$$

where *µ* is the location parameter and σ > 0 is the scale parameter.  Use *µ* = 0 and *σ* = 1 for the standard form of the exponential PDF. It returns NaN for σ = 0.

### *See Also* {#see-also}
[Statistical Analysis](/igorpro/analysis/statistics.md), [StatsExpCDF](/igorpro/commands/statsexpcdf.md), [StatsInvExpCDF](/igorpro/commands/statsinvexpcdf.md)