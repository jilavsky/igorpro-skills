---
description: "The StatsQCDF function returns the value of the Q cumulative distribution function for r the number of groups, c the number of treatments, and df the error…"
slug: /commands/statsqcdf
---

<div className="command-signature">

## <strong>StatsQCDF</strong>  (<em>q</em>, <em>r</em>, <em>c</em>, <em>df</em>) {#statsqcdf}

</div>

The StatsQCDF function returns the value of the Q cumulative distribution function for *r* the number of groups, *c* the number of treatments, and *df* the error degrees of freedom (*f* = *rc* (*n* -1) with sample size *n*).

### *Details* {#details}
The Q distribution is the maximum of several Studentized range statistics. For a simple Tukey test, use *r* =1.

### *References* {#references}
Copenhaver, M.D., and B.S. Holland, Multiple comparisons of simple effects in the two-way analysis of variance with fixed effects, *Journal of Statistical Computation and Simulation*, *30*, 1-15, 1988.

### *See Also* {#see-also}
[Statistical Analysis](/igorpro/analysis/statistics.md), [StatsTukeyTest](/igorpro/commands/statstukeytest.md)