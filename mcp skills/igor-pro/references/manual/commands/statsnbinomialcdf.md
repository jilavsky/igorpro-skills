---
description: "The StatsNBinomialCDF function returns the negative binomial cumulative distribution function."
slug: /commands/statsnbinomialcdf
---

<div className="command-signature">

## <strong>StatsNBinomialCDF</strong> (<em>x</em>, <em>k</em>, <em>p</em>) {#statsnbinomialcdf}

</div>

The StatsNBinomialCDF function returns the negative binomial cumulative distribution function.

$$
\displaystyle F(x ; k, p)={Betai}(k, x+1 ; p),
$$

where [Betai](/igorpro/commands/betai.md) is the regularized incomplete beta function.

### *See Also* {#see-also}
[Statistical Analysis](/igorpro/analysis/statistics.md), [StatsNBinomialPDF](/igorpro/commands/statsnbinomialpdf.md), [StatsInvNBinomialCDF](/igorpro/commands/statsinvnbinomialcdf.md)