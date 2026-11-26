---
description: "The StatsDExpPdf function returns the double-exponential probability distribution function."
slug: /commands/statsdexppdf
---

<div className="command-signature">

## <strong>StatsDExpPdf</strong> (<em>x</em>, µ, σ) {#statsdexppdf}

</div>

The StatsDExpPdf function returns the double-exponential probability distribution function

$$
\displaystyle \mathrm{f}(\mathrm{x} ; \mu, \sigma)=\frac{1}{2 \sigma} \exp \left[-\left|\frac{x-\mu}{\sigma}\right|\right],
$$

where *µ* is the location parameter and σ>0 is the scale parameter. Use *µ*=0 and *σ*=1 for the standard form of the double exponential distribution. It returns NaN when σ=0.

### *See Also* {#see-also}
[Statistical Analysis](/igorpro/analysis/statistics.md), [StatsDExpCDF](/igorpro/commands/statsdexpcdf.md), [StatsInvDExpCDF](/igorpro/commands/statsinvdexpcdf.md)