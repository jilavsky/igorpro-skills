---
description: "The StatsTopDownCDF function returns the cumulative distribution function for the top-down correlation coefficient."
slug: /commands/statstopdowncdf
---

<div className="command-signature">

## <strong>StatsTopDownCDF</strong> (<em>r</em>, <em>N</em>) {#statstopdowncdf}

</div>

The StatsTopDownCDF function returns the cumulative distribution function  for  the top-down correlation coefficient. It is computationally intensive because it must evaluate many permutations [O((*n* !)2)].  It exactly calculates the distribution for 3<=*N* <=7; outside this range it uses Monte-Carlo estimation for 8<=*N* <=50 and asymptotic Normal approximation for *N* >50. The Monte-Carlo estimate uses 1e6 random permutations  fitted with two 9-order polynomials for the range [-1,0] and [0,1]. Results are within 0.2% of exact values where known

### *References* {#references}
Iman, R.L., and W.J. Conover, A measure of top-down correlation, *Technometrics*, *29*, 351-357, 1987.

### *See Also* {#see-also}
[Statistical Analysis](/igorpro/analysis/statistics.md), [StatsRankCorrelationTest](/igorpro/commands/statsrankcorrelationtest.md), [StatsInvTopDownCDF](/igorpro/commands/statsinvtopdowncdf.md)