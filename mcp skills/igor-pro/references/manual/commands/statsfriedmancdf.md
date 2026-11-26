---
description: "The StatsFriedmanCDF function returns the cumulative probability distribution of the Friedman distribution with m rows and n columns."
slug: /commands/statsfriedmancdf
---

<div className="command-signature">

## <strong>StatsFriedmanCDF</strong> (<em>x</em>, <em>n</em>, <em>m</em>, <em>method</em>, <em>useTable</em>) {#statsfriedmancdf}

</div>

The StatsFriedmanCDF function returns the cumulative probability distribution of the Friedman distribution with *m* rows and *n* columns. The exact Friedman distribution is computationally intensive, taking on the order of (*n*!)<sup>*m*</sup> iterations. You may be able to use a range of precomputed exact values by passing a nonzero value for *useTable*, which will use *method* only if the value is not in the table. For large *m*, consider using the Chi-squared or the Monte-Carlo approximations. To abort execution, press the [User Abort Key Combinations](/igorpro/programming/programming.md#user-abort-key-combinations).

| method | What It Does |
| --- | --- |
| 0 | Exact computation |
| 1 | Chi-square approximation |
| 2 | Monte-Carlo approximation |
| 3 | Use built-table only and return NaN if not in table |

### *See Also* {#see-also}
[Statistical Analysis](/igorpro/analysis/statistics.md), [StatsInvFriedmanCDF](/igorpro/commands/statsinvfriedmancdf.md), [StatsFriedmanTest](/igorpro/commands/statsfriedmantest.md)