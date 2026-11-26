---
description: "The StatsMaxwellPDF function returns Maxwell's probability distribution function."
slug: /commands/statsmaxwellpdf
---

<div className="command-signature">

## <strong>StatsMaxwellPDF</strong> (<em>x</em>, <em>k</em>) {#statsmaxwellpdf}

</div>

The StatsMaxwellPDF function returns Maxwell's probability distribution function

$$
\displaystyle f(x ; k)=\sqrt{\frac{2}{\pi}} k^{3 / 2} x^{2} \exp \left(-\frac{k x^{2}}{2}\right), \quad x>0 .
$$

The Maxwell distribution describes, for example, the speed distribution of molecules in an ideal gas.

### *See Also* {#see-also}
[Statistical Analysis](/igorpro/analysis/statistics.md), [StatsMaxwellCDF](/igorpro/commands/statsmaxwellcdf.md), [StatsInvMaxwellCDF](/igorpro/commands/statsinvmaxwellcdf.md)