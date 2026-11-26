---
description: "The StatsNCFPDF function returns the probability distribution function of the noncentral F distribution."
slug: /commands/statsncfpdf
---

<div className="command-signature">

## <strong>StatsNCFPDF</strong> (<em>x</em>, <em>n1</em>, <em>n2</em>, <em>d</em>) {#statsncfpdf}

</div>

The StatsNCFPDF function returns the probability distribution function of the noncentral F distribution.

$$
\displaystyle f\left(x ; n_{1}, n_{2}, d\right)=\frac{\exp (-d / 2)}{B\left(\frac{n_{1}}{2}, \frac{n_{2}}{2}\right)} x^{n_{1} / 2-1}\left(x n_{1}+n_{2}\right)^{-\left(n_{1}+n_{2}\right) / 2} n_{1}^{n_{1} / 2} n_{2}^{n_{2} / 2}{ }_{1} F_{1}\left(\frac{n_{1}+n_{2}}{2}, \frac{n_{1}}{2}, \frac{x d n_{1}}{2\left(x n_{1}+n_{2}\right)}\right),
$$

where *B*() is the [beta](/igorpro/commands/beta.md) function and <sub>1</sub>*F*<sub>1</sub>() is the hypergeometric function [HyperG1F1](/igorpro/commands/hyperg1f1.md).

### *References* {#references}
Abramowitz, M., and I.A. Stegun, "Handbook of Mathematical Functions", 446 pp., Dover, New York, 1972.

Evans, M., N. Hastings, and B. Peacock, *Statistical Distributions*, 3rd ed., Wiley, New York, 2000.

### *See Also* {#see-also}
[Statistical Analysis](/igorpro/analysis/statistics.md), [StatsNCFCDF](/igorpro/commands/statsncfcdf.md), [StatsInvNCFCDF](/igorpro/commands/statsinvncfcdf.md)