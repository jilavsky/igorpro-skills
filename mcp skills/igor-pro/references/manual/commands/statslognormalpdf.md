---
description: "The StatsLogNormalPDF function returns the lognormal probability distribution function."
slug: /commands/statslognormalpdf
---

<div className="command-signature">

## <strong>StatsLogNormalPDF</strong> (<em>x</em>, σ [, θ, µ ]) {#statslognormalpdf}

</div>

The StatsLogNormalPDF function returns the lognormal probability distribution function

$$
\displaystyle f(x ; \sigma, \theta, \mu)=\frac{1}{\sigma \sqrt{2 \pi}} \frac{1}{x-\theta} \exp \left\{-\left[\ln \left(\frac{x-\theta}{\mu}\right)\right]^{2} / 2 \sigma^{2}\right\},
$$

x>*θ* and *σ*, *µ*>0, where *θ* is the location parameter, *µ* is the scale parameter and σ is the shape parameter. The standard lognormal distribution is for *θ* =0 and *µ* =1, which are the optional parameter defaults.

### *References* {#references}
The expression for the PDF follows the NIST definition at https://www.itl.nist.gov/div898/handbook/eda/section3/eda3669.htm. Note that alternate definitions use μ differently.

### *See Also* {#see-also}
[Statistical Analysis](/igorpro/analysis/statistics.md), [StatsLogNormalCDF](/igorpro/commands/statslognormalcdf.md), [StatsInvLogNormalCDF](/igorpro/commands/statsinvlognormalcdf.md)