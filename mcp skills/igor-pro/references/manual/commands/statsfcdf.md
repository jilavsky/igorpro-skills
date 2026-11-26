---
description: "The StatsFCDF function returns the cumulative distribution function for the F distribution with shape parameters n1 and n2."
slug: /commands/statsfcdf
---

<div className="command-signature">

## <strong>StatsFCDF</strong> (<em>x</em>, <em>n1</em>, <em>n2</em>) {#statsfcdf}

</div>

The StatsFCDF function returns the cumulative distribution function for the F distribution with shape parameters *n1* and *n2*

$$
\displaystyle F\left(x ; n_{1}, n_{2}\right)=1-{Betai}\left(\frac{n_{2}}{2}, \frac{n_{1}}{2}, \frac{n_{2}}{n_{2}+n_{1} x}\right),
$$

where *Betai* is the incomplete beta function.

### *See Also* {#see-also}
[Statistical Analysis](/igorpro/analysis/statistics.md), [StatsFPDF](/igorpro/commands/statsfpdf.md), [StatsInvFCDF](/igorpro/commands/statsinvfcdf.md)