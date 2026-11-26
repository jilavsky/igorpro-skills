---
description: "The StatsInvBinomialCDF function returns the inverse of the binomial cumulative distribution function."
slug: /commands/statsinvbinomialcdf
---

<div className="command-signature">

## <strong>StatsInvBinomialCDF</strong> (<em>cdf</em>, <em>p</em>, Ν) {#statsinvbinomialcdf}

</div>

The StatsInvBinomialCDF function returns the inverse of the binomial cumulative distribution function. The inverse function returns the value at which the binomial *CDF* with probability *p* and total elements *N*, has the value 0.95. There is no closed form expression for the inverse binomial CDF; it is evaluated numerically.

### *See Also* {#see-also}
[Statistical Analysis](/igorpro/analysis/statistics.md), [StatsBinomialCDF](/igorpro/commands/statsbinomialcdf.md), [StatsBinomialPDF](/igorpro/commands/statsbinomialpdf.md)