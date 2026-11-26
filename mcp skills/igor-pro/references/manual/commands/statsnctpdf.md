---
description: "The StatsNCTPDF function returns the probability distribution function of the noncentral Student-T distribution."
slug: /commands/statsnctpdf
---

<div className="command-signature">

## <strong>StatsNCTPDF</strong> (<em>x</em>, <em>df</em>, <em>d</em>) {#statsnctpdf}

</div>

The StatsNCTPDF function returns the probability distribution function of the noncentral Student-T distribution. *df* is the degrees of freedom (positive integer) and *d* is the noncentrality measure.

$$
\displaystyle f(x ; n, \delta)=\frac{n^{n / 2} n!}{2^{n} e^{\delta^{2} / 2}\left(n+x^{2}\right)^{n / 2} \Gamma\left(\frac{n}{2}\right)}\left\{\frac{\sqrt{2} \delta x_{1} F_{1}\left(\frac{n}{2}+1 ; \frac{3}{2} ; \frac{\delta^{2} x^{2}}{2\left(n+x^{2}\right)}\right)}{\left(n+x^{2}\right) \Gamma\left(\frac{n+1}{2}\right)}+\frac{{ }_{1} F_{1}\left(\frac{n+1}{2} ; \frac{1}{2} ; \frac{\delta^{2} x^{2}}{2\left(n+x^{2}\right)}\right)}{\sqrt{\left(n+x^{2}\right)} \Gamma\left(\frac{n}{2}+1\right)}\right\}
$$

### *References* {#references}
Evans, M., N. Hastings, and B. Peacock, *Statistical Distributions*, 3rd ed., Wiley, New York, 2000.

### *See Also* {#see-also}
[Statistical Analysis](/igorpro/analysis/statistics.md), [StatsStudentCDF](/igorpro/commands/statsstudentcdf.md), [StatsStudentPDF](/igorpro/commands/statsstudentpdf.md), [StatsNCTCDF](/igorpro/commands/statsnctcdf.md)