---
description: "The StatsBinomialCDF function returns the binomial cumulative distribution function."
slug: /commands/statsbinomialcdf
---

<div className="command-signature">

## <strong>StatsBinomialCDF</strong> (<em>x</em>, <em>p</em>, Ν) {#statsbinomialcdf}

</div>

The StatsBinomialCDF function returns the binomial cumulative distribution function

$$
\displaystyle F(x ; p, N)=\sum_{i=1}^{x}\binom{N}{i} p^{i}(1-p)^{N-i}, \quad x=1,2, \ldots
$$

where

$$
\displaystyle \binom{N}{i}=\frac{N!}{i!(N-i)!} .
$$

### *See Also* {#see-also}
[Statistical Analysis](/igorpro/analysis/statistics.md), [StatsBinomialPDF](/igorpro/commands/statsbinomialpdf.md), [StatsInvBinomialCDF](/igorpro/commands/statsinvbinomialcdf.md)