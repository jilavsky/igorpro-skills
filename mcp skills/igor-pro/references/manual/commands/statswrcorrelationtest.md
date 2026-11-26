---
description: "The StatsWRCorrelationTest operation performs a Weighted Rank Correlation test on waveA and waveB, which contain the ranks of sequential factors."
slug: /commands/statswrcorrelationtest
---

<div className="command-signature">

## <strong>StatsWRCorrelationTest</strong>  [/ALPH=<em>val</em> /T=<em>k</em> /Z/Q]  <em>waveA</em>, <em>waveB</em> {#statswrcorrelationtest}

</div>

The StatsWRCorrelationTest operation performs a Weighted Rank Correlation test on waveA and waveB, which contain the ranks of sequential factors. The waves are 1-based, integer ranks of factors in the range 1-2^31.

StatsWRCorrelationTest computes a top-down correlation coefficient using Savage sums as well as the critical and P-values. Output is to the W_StatsWRCorrelationTest wave in the current data folder or optionally to a table.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/ALPH = *val*</span> | Sets the significance level (default *val* =0.05). |
| <span class="table-cell-nowrap">/DEST = *dstWave*</span> | Specify the destination wave for the Weighted Rank Correlation test results.  If you do not use this flag, the results are stored in the wave W_StatsWRCorrelationTest in the current data folder. |
|  | This flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/FREE</span> | Creates the user-specified destination wave as a free wave. |
|  | /FREE is allowed only in functions, and only if the destination waves are simple names or wave reference structure fields. |
|  | See [Free Waves](/igorpro/programming/programming.md#free-waves) for more discussion. |
|  | The /FREE flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/Q</span> | No results printed in the history area. |
| <span class="table-cell-nowrap">/T = *k*</span> | Displays results in a table. *k*  specifies the table behavior when it is closed. |
|  |<table class="nested-table"><tbody><tr><td>*k*&nbsp;=0:</td><td>Normal with dialog (default).</td></tr><tr><td>*k*&nbsp;=1:</td><td>Kills with no dialog.</td></tr><tr><td>*k*&nbsp;=2:</td><td>Disables killing.</td></tr></tbody></table>
|  | The table is associated with the test, not the data. If you repeat the test, it will update any existing table with the new results. |
| <span class="table-cell-nowrap">/Z</span> | Ignores errors. V_flag will be set to -1 for any error and to zero otherwise. |

### *Details* {#details}
The StatsWRCorrelationTest input waves must be one-dimensional and have the same length. The waves are 1-based, integer ranks of factors corresponding to the point number. Ranks may have ties in which case you should repeat the rank value. For example, if the second and third entries have the same rank you should enter {1,2,2,4}. H<sub>0</sub> stipulates that the same factors are most important in both groups represented by *waveA*  and *waveB*.

The top-down correlation is the sum of the product of Savage sums for each row:

$$
r_{T D}=\frac{\displaystyle \sum_{i=1}^{n} S_{i A} S_{i B}-n}{n-S_{1}},
$$

where *n*  is the number of rows and the Savage sum *S*<sub>i</sub>  is

$$
\displaystyle S_{i}=\sum_{j=i}^{n} \frac{1}{j},
$$

and *S*<sub>iA</sub>  corresponds to the *S*<sub>i</sub>  value of the rank of the data in row (*i* -1) of *waveA*.

### *References* {#references}
Iman, R.L., and W.J. Conover, A measure of top-down correlation, *Technometrics*, *29*, 351-357, 1987.

See, in particular, Chapter 19 of:

Zar, J.H., *Biostatistical Analysis*, 4th ed., 929 pp., Prentice Hall, Englewood Cliffs, New Jersey, 1999.

### *See Also* {#see-also}
[Statistical Analysis](/igorpro/analysis/statistics.md), [StatsLinearCorrelationTest](/igorpro/commands/statslinearcorrelationtest.md), [StatsRankCorrelationTest](/igorpro/commands/statsrankcorrelationtest.md), [StatsTopDownCDF](/igorpro/commands/statstopdowncdf.md), [StatsInvTopDownCDF](/igorpro/commands/statsinvtopdowncdf.md)

### *Demos* {#demos}
[Open WR Correlation Demo.pxp](#igor-pxp/Examples/Statistics/WR__Correlation__Demo.pxp)