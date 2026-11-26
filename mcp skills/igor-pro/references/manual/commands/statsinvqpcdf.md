---
description: "The StatsInvQpCDF function returns the critical value of the Q' cumulative distribution function for ng the number of groups, nt the number of treatments, and…"
slug: /commands/statsinvqpcdf
---

<div className="command-signature">

## <strong>StatsInvQpCDF</strong> (<em>ng</em>, <em>nt</em>, <em>df</em>, <em>alpha</em>, <em>side</em>, <em>sSizeWave</em>) {#statsinvqpcdf}

</div>

The StatsInvQpCDF function returns the critical value of the Q' cumulative distribution function for *ng* the number of groups, *nt* the number of treatments, and *df* the error degrees of freedom. *side* =1 for upper-tail or *side* =2 for two-tailed critical values.

*sSizeWave* is an integer wave of *ng* columns and *nt* rows specifying the number of samples in each treatment. If *sSizeWave* is a null wave ($""), StatsInvQpCDF computes the number of samples from:

```igor
df = ng * nt * (n - 1) 
```

with *n* truncated to an integer.

### *Details* {#details}
StatsInvQpCDF is a modified Q distribution typically used with Dunnett's test, which compares the various means with the mean of the control group or treatment.

StatsInvQpCDF differs from other StatsInv*XXX* functions in that you do not specify a *cdf* value for the inverse (usually 1-*alpha* for the critical value). Here *alpha* selects one- or two-tailed critical values.

It is computationally intensive, taking longer to execute for smaller *alpha* values.

### *Examples* {#examples}
The critical value for a Dunnett test comparing 4 treatments with 4 samples and (upper tail) 0.05 significance is:


```igor
// n=4 because 12=1*4*(4-1).
Print StatsInvQpCDF(1,4,12,0.05,1,$"")
  2.28734
```

### *See Also* {#see-also}
[Statistical Analysis](/igorpro/analysis/statistics.md), [StatsDunnettTest](/igorpro/commands/statsdunnetttest.md), [StatsInvQCDF](/igorpro/commands/statsinvqcdf.md)