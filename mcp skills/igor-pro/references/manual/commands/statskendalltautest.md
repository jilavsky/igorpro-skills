---
description: "The StatsKendallTauTest operation performs the nonparametric Mann-Kendall test, which computes a correlation coefficient τ (similar to Spearman's correlation)…"
slug: /commands/statskendalltautest
---

<div className="command-signature">

## <strong>StatsKendallTauTest</strong>  [/Q/Z] [/T=<em>k</em>]  <em>wave1</em> [,<em>wave2</em>] {#statskendalltautest}

</div>

The StatsKendallTauTest operation performs the nonparametric Mann-Kendall test, which computes a correlation coefficient τ (similar to Spearman's correlation) from the relative order of the ranks of the data. Output is to the W_StatsKendallTauTest wave in the current data folder.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/DEST = *ktWave*</span> | Specify the destination wave for the test results.  If you do not specify this flag, the operation saves this output in the wave W_StatsKendallTauTest in the current data folder. |
|  | This flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/FREE</span> | Creates the user-specified destination wave as a free wave. |
|  | /FREE is allowed only in functions, and only if the destination waves are simple names or wave reference structure fields. |
|  | See [Free Waves](/igorpro/programming/programming.md#free-waves) for more discussion. |
|  | The /FREE flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/Q</span> | No results printed in the history area. |
| <span class="table-cell-nowrap">/T = *k*</span> | Displays results in a table. *k* specifies the table behavior when it is closed. |
|  |<table class="nested-table"><tbody><tr><td>*k*&nbsp;=0:</td><td>Normal with dialog (default).</td></tr><tr><td>*k*&nbsp;=1:</td><td>Kills with no dialog.</td></tr><tr><td>*k*&nbsp;=2:</td><td>Disables killing.</td></tr></tbody></table>
| <span class="table-cell-nowrap">/Z</span> | Ignores errors. V_flag will be set to -1 for any error and to zero otherwise. |

### *Details* {#details}
Inputs may be a pair of XY (1D) waves of any real numeric type or a single 1D wave, which is equivalent to using a pair of XY waves where the X wave is monotonically increasing function of the point number. StatsKendallTauTest ignores wave scaling.

Kendall's τ is 1 for a monotonically increasing input and -1 for monotonically decreasing input. The significance of the test is computed from the normal approximation

$$
\displaystyle \operatorname{Var}(\tau)=\frac{4 n+10}{9 n(n-1)},
$$

where *n* is the number of data points in each wave. The significance is expressed as a P-value for the null hypothesis of no correlation.

### *References* {#references}
Kendall, M.G., *Rank Correlation Methods*, 3rd ed., Griffin, London, 1962.

### *See Also* {#see-also}
[Statistical Analysis](/igorpro/analysis/statistics.md), [StatsRankCorrelationTest](/igorpro/commands/statsrankcorrelationtest.md)

For small values of n you can compute the exact probability using the procedure WM_KendallSProbability().