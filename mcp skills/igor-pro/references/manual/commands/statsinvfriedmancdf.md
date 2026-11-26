---
description: "The StatsInvFriedmanCDF function returns the inverse of the Friedman distribution cumulative distribution function of cdf with m rows and n columns."
slug: /commands/statsinvfriedmancdf
---

<div className="command-signature">

## <strong>StatsInvFriedmanCDF</strong> (<em>cdf</em>, <em>n</em>, <em>m</em>, <em>method</em>, <em>useTable</em>) {#statsinvfriedmancdf}

</div>

The StatsInvFriedmanCDF function returns the inverse of the Friedman distribution cumulative distribution function of *cdf* with *m* rows and *n* columns. Use this  typically to compute the critical values of the distribution


```igor
Print StatsInvFriedmanCDF(1-alpha,n,m,0,1)
```

where alpha is the significance level of the associated test.

The complexity of the computation of Friedman CDF is on the order of (*n*!)^*m*. For nonzero values of *useTable*, searches are limited to the built-in table for distribution values. If *n* and *m* are not in the table the calculation may still proceed according to the method.

| method | What It Does |
| --- | --- |
| 0 | Exact computation(slow, not recommended). |
| 1 | Chi-square approximation |
| 2 | Monte-Carlo approximation (slow) |
| 3 | Use built-in table only and return a NaN if not in table. |

For large *m* and *n*, consider using the Chi-squared or the Iman and Davenport approximations. To abort execution, press the [User Abort Key Combinations](/igorpro/programming/programming.md#user-abort-key-combinations).

:::note
Table values are different from computed values for both methods. Table values use more conservative criteria than computed values. Table values are more consistent with published values because the Friedman distribution is a highly irregular function with multiple steps of arbitrary sizes. The standard for published tables provides the X value of the next vertical transition to the one on which the specified P is found.
:::

Precomputed tables use these values:

| n | m |
| --- | --- |
| 3 | 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16 |
| 4 | 2, 3, 4, 5, 6, 7, 8, 9 |
| 5 | 2, 3, 4, 5, 6 |
| 6 | 2, 3, 4, 5 |
| 7 | 2, 3, 4 |
| 8 | 2, 3 |
| 9 | 2, 3 |

### *References* {#references}
Iman, R.L., and J.M. Davenport, Approximations of the critical region of the Friedman statistic, *Comm. Statist*., *A9*, 571-595, 1980.

### *See Also* {#see-also}
[Statistical Analysis](/igorpro/analysis/statistics.md), [StatsFriedmanCDF](/igorpro/commands/statsfriedmancdf.md), [StatsFriedmanTest](/igorpro/commands/statsfriedmantest.md)