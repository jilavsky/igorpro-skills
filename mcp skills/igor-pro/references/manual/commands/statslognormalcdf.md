---
description: "The StatsLogNormalCDF function returns the lognormal cumulative distribution function."
slug: /commands/statslognormalcdf
---

<div className="command-signature">

## <strong>StatsLogNormalCDF</strong> (<em>x</em>, σ [, θ, µ ]) {#statslognormalcdf}

</div>

The StatsLogNormalCDF function returns the lognormal cumulative distribution function

$$
\displaystyle F(x ; \sigma, \theta, \mu)=\frac{1}{\sigma \sqrt{2 \pi}} \int_{0}^{x} \frac{1}{t-\theta} \exp \left\{-\left[\ln \left(\frac{t-\theta}{\mu}\right)\right]^{2} / 2 \sigma^{2}\right\} d t,
$$

for x>*θ* and *σ*, *µ*>0. The standard lognormal distribution is for *θ* =0 and *µ* =1, which are the optional parameter defaults

### *See Also* {#see-also}
[Statistical Analysis](/igorpro/analysis/statistics.md), [StatsLogNormalPDF](/igorpro/commands/statslognormalpdf.md), [StatsInvLogNormalCDF](/igorpro/commands/statsinvlognormalcdf.md)