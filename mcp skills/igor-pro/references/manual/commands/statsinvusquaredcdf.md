---
description: "The StatsInvUSquaredCDF function returns the inverse of Watson's U2 cumulative distribution function integer sample sizes n and m."
slug: /commands/statsinvusquaredcdf
---

<div className="command-signature">

## <strong>StatsInvUSquaredCDF</strong> (<em>cdf</em>, <em>n</em>, <em>m</em>, <em>method</em>, <em>useTable</em>) {#statsinvusquaredcdf}

</div>

The StatsInvUSquaredCDF function returns the inverse of Watson's U<sup>2</sup> cumulative distribution function integer sample sizes *n* and *m*. Use a nonzero value for *useTable* to search a built-in table of values. If *n* and *m* cannot be found in the table, it will proceed according to *method :*

| method | What It Does |
| --- | --- |
| 0 | Exact computation using Burr algorithm (could be slow). |
| 1 | Tiku approximation using chi-squared. |
| 2 | Use built-in table only and return a NaN if not in table. |

For large *n* and *m*, consider using the Tiku approximation. To abort execution, press the [User Abort Key Combinations](/igorpro/programming/programming.md#user-abort-key-combinations). Because *n* and *m* are interchangeable, *n* should always be the smaller value. For *n* >8 the upper limit in the table matched the maximum that can be computed using the Burr algorithm. There is no point in using method 0 with *m* values exceeding these limits.

The inverse is obtained from precomputed tables of Watson's U<sup>2</sup> (see [StatsUSquaredCDF](/igorpro/commands/statsusquaredcdf.md)).

:::note
Table values are different from computed values. These values use more conservative criteria than computed values. Table values are more consistent with published values because the U2 distribution is a highly irregular function with multiple steps of arbitrary sizes. The standard for published tables provides the X value of the next vertical transition to the one on which the specified P is found. See StatsInvFriedmanCDF.
:::

### *References* {#references}
Burr, E.J., Small sample distributions of the two sample Cramer-von Mises' W<sup>2</sup> and Watson's U<sup>2</sup>, *Ann. Mah. Stat. Assoc.*, *64*, 1091-1098, 1964.

Tiku, M.L., Chi-square approximations for the distributions of goodness-of-fit statistics, *Biometrica*, *52*, 630-633, 1965.

### *See Also* {#see-also}
[Statistical Analysis](/igorpro/analysis/statistics.md), [StatsWatsonUSquaredTest](/igorpro/commands/statswatsonusquaredtest.md), [StatsUSquaredCDF](/igorpro/commands/statsusquaredcdf.md)