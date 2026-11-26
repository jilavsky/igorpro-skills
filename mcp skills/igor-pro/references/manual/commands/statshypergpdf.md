---
description: "The StatsHyperGPDF function returns the hypergeometric probability distribution function, which is the probability of getting x marked items when drawing…"
slug: /commands/statshypergpdf
---

<div className="command-signature">

## <strong>StatsHyperGPDF</strong> (<em>x</em>, <em>m</em>, <em>n</em>, <em>k</em>) {#statshypergpdf}

</div>

The StatsHyperGPDF function returns the hypergeometric probability distribution function, which is the probability of getting *x* marked items when drawing without replacement *k* items out of a population of *m* items where *n* out of the *m* are marked.

### *Details* {#details}
The hypergeometric distribution is

$$
f(x ; m, n, k)=\frac{\displaystyle \binom{n}{x}\binom{m-n}{k-x}}{\displaystyle \binom{m}{k}},
$$

where 
$$
\displaystyle \binom{a}{b}
$$
 is the [binomial](/igorpro/commands/binomial.md) function. All parameters must be positive integers and must have  *m* >*n* and *x* <*k.*

### *References* {#references}
J.H. Klotz, *Computational Approach to Statistics*.

### *See Also* {#see-also}
[Statistical Analysis](/igorpro/analysis/statistics.md), [StatsHyperGCDF](/igorpro/commands/statshypergcdf.md)