---
description: "The StatsWatsonUSquaredTest operation performs Watson's nonparametric two-sample U2 test for samples of circular data."
slug: /commands/statswatsonusquaredtest
---

<div className="command-signature">

## <strong>StatsWatsonUSquaredTest</strong>  [/ALPH=<em>val</em> /Q/Z/T=<em>k</em>]  <em>srcWave1</em>, <em>srcWave2</em> {#statswatsonusquaredtest}

</div>

The StatsWatsonUSquaredTest operation performs Watson's nonparametric two-sample U<sup>2</sup> test for samples of circular data. Output is to the W_WatsonUtest wave in the current data folder or optionally to a table.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/ALPH = *val*</span> | Sets the significance level (default *val* =0.05). |
| <span class="table-cell-nowrap">/DEST = *sWave*</span> | Specify the destination wave for Watson's non-parametric two sample test results.  If you do not use this flag, the operation saves this output in the wave W_WatsonUtest in the current data folder. |
|  | This flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/FREE</span> | Creates the user-specified destination wave as a free wave. |
|  | /FREE is allowed only in functions, and only if the destination waves are simple names or wave reference structure fields. |
|  | See [Free Waves](/igorpro/programming/programming.md#free-waves) for more discussion. |
|  | The /FREE flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/Q</span> | No results printed in the history area. |
| <span class="table-cell-nowrap">/T = *k*</span> | Displays results in a table. *k* specifies the table behavior when it is closed. |
|  |<table class="nested-table"><tbody><tr><td>*k*&nbsp;=0:</td><td>Normal with dialog (default).</td></tr><tr><td>*k*&nbsp;=1:</td><td>Kills with no dialog.</td></tr><tr><td>*k*&nbsp;=2:</td><td>Disables killing.</td></tr></tbody></table>
|  | The table is associated with the test, not the data. If you repeat the test, it will update any existing table with the new results. |
| <span class="table-cell-nowrap">/Z</span> | Ignores errors. V_flag will be set to -1 for any error and to zero otherwise. |

### *Details* {#details}
The input waves, *srcWave1* and *srcWave2*, each must contain at least two angles in radians (mod 2π) can have any number of dimensions, and can be single or double precision. They must not contain NaNs or INFs.

The Watson U<sup>2</sup> H<sub>0</sub> postulates that the two samples came from the same population against the different populations alternative. In the calculation, StatsWatsonUSquaredTest ranks the two inputs, accounts for possible ties, computes the test statistic U<sup>2</sup>, and compares it with the critical value. Because of the difficulty of computing the critical values, it always computes first the approximation due to Tiku and if possible it computes the exact critical value using the method outlined by Burr. You can evaluate the U<sup>2</sup> CDF to get more information about the critical region.

V_flag will be set to -1 for any error and to zero otherwise.

### *References* {#references}
We have found that this method leads to slightly different results depending on the compiler and the system on which it is implemented:

Burr, E.J., Small sample distributions of the two sample Cramer-von Mises' W2 and Watson's U2, *Ann. Mah. Stat. Assoc.*, *64*, 1091-1098, 1964.

Tiku, M.L., Chi-square approximations for the distributions of goodness-of-fit statistics, *Biometrica*, *52*, 630-633, 1965.

### *See Also* {#see-also}
[Statistical Analysis](/igorpro/analysis/statistics.md), [StatsWatsonWilliamsTest](/igorpro/commands/statswatsonwilliamstest.md), [StatsWheelerWatsonTest](/igorpro/commands/statswheelerwatsontest.md), [StatsUSquaredCDF](/igorpro/commands/statsusquaredcdf.md), [StatsInvUSquaredCDF](/igorpro/commands/statsinvusquaredcdf.md)

### *Demos* {#demos}
[Open Watson USquared Demo.pxp](#igor-pxp/Examples/Statistics/Circular__Statistics/Watson__USquared__Demo.pxp)