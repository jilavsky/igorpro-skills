---
description: "The StatsInvTopDownCDF function returns the inverse cumulative distribution function for the top-down distribution."
slug: /commands/statsinvtopdowncdf
---

<div className="command-signature">

## <strong>StatsInvTopDownCDF</strong> (<em>cdf</em>, <em>N</em>) {#statsinvtopdowncdf}

</div>

The StatsInvTopDownCDF function returns the inverse cumulative distribution function for the top-down distribution. For 3<=*N* <=7 it uses a lookup table CDF and returns the next higher value of r for which the distribution value is larger than cdf. For 8<=*N* <=50 it returns the nearest value for which the built-in distribution returns *cdf*. For *N* >50 it returns the scaled normal approximation.

Tabulated values are from Iman and Conover who pick as the critical value the very first transition of the distribution following the specified *cdf* value. These tabulated values tend to be slightly higher than calculated values for 7<*N* <15

### *References* {#references}
Iman, R.L., and W.J. Conover, A measure of top-down correlation, *Technometrics*, *29*, 351-357, 1987.

### *See Also* {#see-also}
[Statistical Analysis](/igorpro/analysis/statistics.md), [StatsRankCorrelationTest](/igorpro/commands/statsrankcorrelationtest.md), [StatsTopDownCDF](/igorpro/commands/statstopdowncdf.md)