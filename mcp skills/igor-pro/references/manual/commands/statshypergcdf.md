---
description: "The StatsHyperGCDF function returns the hypergeometric cumulative distribution function, which is the probability of getting x marked items when drawing…"
slug: /commands/statshypergcdf
---

<div className="command-signature">

## <strong>StatsHyperGCDF</strong> (<em>x</em>, <em>m</em>, <em>n</em>, <em>k</em>) {#statshypergcdf}

</div>

The StatsHyperGCDF function returns the hypergeometric cumulative distribution function, which is the probability of getting *x* marked items when drawing (without replacement) *k* items out of a population of *m* items when *n* out of the *m* are marked.

### *Details* {#details}
The hypergeometric distribution is

$$
F(x ; m, n, k)=\sum_{L=0}^{x} \frac{\displaystyle \binom{n}{L}\binom{m-L}{k-L}}{\displaystyle \binom{m}{k}},
$$

where 
$$
\displaystyle \binom{a}{b}
$$
 is the [binomial](/igorpro/commands/binomial.md) function. All parameters must be positive integers and must have  *m* >*n* and *x* <*k* ; otherwise it returns NaN.

### *References* {#references}
J.H. Klotz, *Computational Approach to Statistics*.

### *See Also* {#see-also}
[Statistical Analysis](/igorpro/analysis/statistics.md), [StatsHyperGPDF](/igorpro/commands/statshypergpdf.md)