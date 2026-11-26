---
description: "The StatsMaxwellCDF function returns the Maxwell cumulative distribution function."
slug: /commands/statsmaxwellcdf
---

<div className="command-signature">

## <strong>StatsMaxwellCDF</strong> (<em>x</em>, <em>k</em>) {#statsmaxwellcdf}

</div>

The StatsMaxwellCDF function returns the Maxwell cumulative distribution function

$$
\displaystyle F(x ; k)= { gammp }\left(\frac{3}{2}, \frac{k x^{2}}{2}\right), \quad x>0 .
$$

where [gammp](/igorpro/commands/gammp.md) is the regularized incomplete gamma function.

### *See Also* {#see-also}
[Statistical Analysis](/igorpro/analysis/statistics.md), [StatsMaxwellPDF](/igorpro/commands/statsmaxwellpdf.md), [StatsInvMaxwellCDF](/igorpro/commands/statsinvmaxwellcdf.md)