---
description: "The StatsInvQCDF function returns the critical value of the Q cumulative distribution function for r the number of groups, c the number of treatments, and df…"
slug: /commands/statsinvqcdf
---

<div className="command-signature">

## <strong>StatsInvQCDF</strong>  (<em>cdf</em>, <em>r</em>, <em>c</em>, <em>df</em>) {#statsinvqcdf}

</div>

The StatsInvQCDF function returns the critical value of the Q cumulative distribution function for *r* the number of groups, *c* the number of treatments, and *df* the error degrees of freedom (*df* = *r* \* *c* \* (*n* -1) with sample size *n*).

### *Details* {#details}
The Q distribution is the maximum of several Studentized range statistics. For a simple Tukey test, use *r* =1.

### *Examples* {#examples}
The critical value for a Tukey test comparing 5 treatments with 6 samples and 0.05 significance is:


```igor
Print StatsInvQCDF(1-0.05,1,5,5*(6-1))
```

### *See Also* {#see-also}
[Statistical Analysis](/igorpro/analysis/statistics.md), [StatsTukeyTest](/igorpro/commands/statstukeytest.md)