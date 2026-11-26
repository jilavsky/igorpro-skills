---
description: "The StatsWaldPDF function returns the inverse Gaussian or Wald probability distribution function."
slug: /commands/statswaldpdf
---

<div className="command-signature">

## <strong>StatsWaldPDF</strong> (<em>x</em>, µ, λ) {#statswaldpdf}

</div>

The StatsWaldPDF function returns the inverse Gaussian or Wald probability distribution function

$$
\displaystyle f(x ; \mu, \lambda)=\sqrt{\frac{\lambda}{2 \pi x^{3}}} \exp \left[-\frac{\lambda(x-\mu)^{2}}{2 \mu^{2} x}\right] .
$$

where *x*, *µ*, *λ > 0.*

### *See Also* {#see-also}
[Statistical Analysis](/igorpro/analysis/statistics.md), [StatsWaldCDF](/igorpro/commands/statswaldcdf.md)