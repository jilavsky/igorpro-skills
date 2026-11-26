---
description: "The StatsBinomialPDF function returns the binomial probability distribution function."
slug: /commands/statsbinomialpdf
---

<div className="command-signature">

## <strong>StatsBinomialPDF</strong> (<em>x</em>, <em>p</em>, Ν) {#statsbinomialpdf}

</div>

The StatsBinomialPDF function returns the binomial probability distribution function

$$
\displaystyle f(x ; p, N)=\binom{N}{x} p^{x}(1-p)^{N-x}, \quad x=0,1,2, \ldots
$$

where

$$
\displaystyle \binom{N}{x}=\frac{N!}{x!(N-x)!} .
$$

is the probability of obtaining *x* "good" outcomes in *N* trials where the probability of a single successful outcome is *p*.

### *See Also* {#see-also}
[Statistical Analysis](/igorpro/analysis/statistics.md), [StatsBinomialCDF](/igorpro/commands/statsbinomialcdf.md), [StatsInvBinomialCDF](/igorpro/commands/statsinvbinomialcdf.md)