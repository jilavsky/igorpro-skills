---
description: "The StatsNCChiPDF function returns the noncentral chi-squared probability distribution function."
slug: /commands/statsncchipdf
---

<div className="command-signature">

## <strong>StatsNCChiPDF</strong> (<em>x</em>, <em>n</em>, <em>d</em>) {#statsncchipdf}

</div>

The StatsNCChiPDF function returns the noncentral chi-squared probability distribution function.

$$
f(x ; n, d)=\frac{\sqrt{d} \exp \displaystyle \left(-\frac{x+d}{2}\right) x^{(n-1) / 2}}{2(d x)^{n / 4}} I_{n / 2-1}(\sqrt{d x}) .
$$

where *n* > 0 corresponds to degrees of freedom, *d* >= 0 is the noncentrality parameter, and *I*<sub>k </sub>(*x*) is the modified Bessel function of the first kind, [bessI](/igorpro/commands/bessi.md).

### *See Also* {#see-also}
[Statistical Analysis](/igorpro/analysis/statistics.md), [StatsNCChiCDF](/igorpro/commands/statsncchicdf.md), [StatsInvNCChiCDF](/igorpro/commands/statsinvncchicdf.md), [StatsChiPDF](/igorpro/commands/statschipdf.md), [StatsChiCDF](/igorpro/commands/statschicdf.md)