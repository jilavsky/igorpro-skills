---
description: "The StatsQpCDF function returns the Q' cumulative distribution function associated with Dunnett's test."
slug: /commands/statsqpcdf
---

<div className="command-signature">

## <strong>StatsQpCDF</strong> (<em>q</em>, <em>nr</em>, <em>nt</em>, <em>df</em>, <em>side</em>, <em>sSizeWave</em>) {#statsqpcdf}

</div>

The StatsQpCDF function returns the Q' cumulative distribution function associated with Dunnett's test.

Here *nr* is the number of groups (should be set to 1), *nt* is the number of treatments, *df* is the error degrees of freedom.

Set *side* =1 for upper-tail or *side* =2 for two-tailed CDF.

*sSizeWave* is an integer wave of *nt* rows specifying the number of samples in each treatment.

### *Details* {#details}
StatsQpCDF is a modified Q distribution typically used with Dunnett's test, which compares the various means with the mean of the control group or treatment.

### *Reference* {#reference}
"Algorithm AS 251: Multivariate Normal Probability Integrals with Product Correlations Structure", C. W. Dunnett, Appl. Stat., **38** (1989) 564-579.

A short correction for the algorithm was published in: Appl. Stat., **42** (1993) 709.

### *See Also* {#see-also}
[Statistical Analysis](/igorpro/analysis/statistics.md), [StatsDunnettTest](/igorpro/commands/statsdunnetttest.md), [StatsInvQpCDF](/igorpro/commands/statsinvqpcdf.md), [StatsInvQCDF](/igorpro/commands/statsinvqcdf.md)