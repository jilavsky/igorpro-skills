---
description: "The StatsFPDF function returns the probability distribution function for the F distribution with shape parameters n1 and n2."
slug: /commands/statsfpdf
---

<div className="command-signature">

## <strong>StatsFPDF</strong> (<em>x</em>, <em>n1</em>, <em>n2</em>) {#statsfpdf}

</div>

The StatsFPDF function returns the probability distribution function for the F distribution with shape parameters *n1* and *n2*

$$
\displaystyle f\left(x ; n_{1}, n_{2}\right)=\frac{\Gamma\left(\frac{n_{1}+n_{2}}{2}\right)\left(\frac{n_{1}}{n_{2}}\right)^{\frac{n_{1}}{2}} x^{\frac{n_{1}}{2}-1}}{\Gamma\left(\frac{n_{1}}{2}\right) \Gamma\left(\frac{n_{2}}{2}\right)\left(1+\frac{n_{1} x}{n_{2}}\right)^{\frac{n_{1}+n_{2}}{2}}} .
$$

### *See Also* {#see-also}
[Statistical Analysis](/igorpro/analysis/statistics.md), [StatsFCDF](/igorpro/commands/statsfcdf.md), [StatsInvFCDF](/igorpro/commands/statsinvfcdf.md)