---
description: "The StatsNBinomialPDF function returns the negative binomial probability distribution function."
slug: /commands/statsnbinomialpdf
---

<div className="command-signature">

## <strong>StatsNBinomialPDF</strong> (<em>x</em>, <em>k</em>, <em>p</em>) {#statsnbinomialpdf}

</div>

The StatsNBinomialPDF function returns the negative binomial probability distribution function.

$$
\displaystyle f(x ; k, p)=\binom{x+k-1}{k-1} p^{k}(1-p)^{x}, \quad x=0,1,2 \ldots
$$

where  
$$
\displaystyle \binom{a}{b}
$$
 is the [binomial](/igorpro/commands/binomial.md) function.

The binomial distribution expresses the probability of the *k* th success in the *x*+*k* trial for two mutually exclusive results (success and failure) and *p* the probability of success in a single trial.

### *See Also* {#see-also}
[Statistical Analysis](/igorpro/analysis/statistics.md), [StatsNBinomialCDF](/igorpro/commands/statsnbinomialcdf.md), [StatsInvNBinomialCDF](/igorpro/commands/statsinvnbinomialcdf.md)