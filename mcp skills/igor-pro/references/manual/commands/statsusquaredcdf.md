---
description: "The StatsUSquaredCDF function returns the cumulative distribution function for Watson's U2 with parameters u2 (U2 statistic) and integer sample sizes n and m."
slug: /commands/statsusquaredcdf
---

<div className="command-signature">

## <strong>StatsUSquaredCDF</strong> (<em>u2</em>, <em>n</em>, <em>m</em>, <em>method</em>, <em>useTable</em>) {#statsusquaredcdf}

</div>

The StatsUSquaredCDF function returns the cumulative distribution function for Watson's U<sup>2</sup> with parameters *u2* (U<sup>2</sup> statistic) and integer sample sizes *n* and *m*. The calculation is computationally intensive, on the order of binomial(*n* +*m*, *m* ). Use a nonzero value for *useTable* to search a built-in table of values. If *n* and *m* cannot be found in the table, it will proceed according to *method* :

| method | What It Does |
| --- | --- |
| 0 | Exact computation using Burr algorithm (could be slow). |
| 1 | Tiku approximation using chi-squared. |
| 2 | Use built-in table only and return a NaN if not in table. |


For large *n* and *m*, consider using the Tiku approximation. To abort execution, press the [User Abort Key Combinations](/igorpro/programming/programming.md#user-abort-key-combinations).

Precomputed tables, using the algorithm described by Burr, contain these values:

| n | m |
| --- | --- |
| 4 | 4-30 |
| 5 | 5-30 |
| 6 | 6-30 |
| 7 | 7-30 |
| 8 | 8-26 |
| 9 | 9-22 |
| 10 | 10-18 |
| 11 | 11-16 |
| 12 | 12-14 |
| 13 | 13 |

Because *n* and *m* are interchangeable, *n* should always be the smaller value. For *n*>8 the upper limit in the table matched the maximum that can be computed using the Burr algorithm. There is no point in using method 0 with *m* values exceeding these limits.

### *References* {#references}
Burr, E.J., Small sample distributions of the two sample Cramer-von Mises' W<sup>2</sup> and Watson's U<sup>2</sup>, *Ann. Mah. Stat. Assoc.*, *64*, 1091-1098, 1964.

Tiku, M.L., Chi-square approximations for the distributions of goodness-of-fit statistics, *Biometrica*, *52*, 630-633, 1965.

### *See Also* {#see-also}
[Statistical Analysis](/igorpro/analysis/statistics.md), [StatsWatsonUSquaredTest](/igorpro/commands/statswatsonusquaredtest.md), [StatsInvUSquaredCDF](/igorpro/commands/statsinvusquaredcdf.md)