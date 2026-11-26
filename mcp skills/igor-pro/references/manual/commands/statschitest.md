---
description: "The StatsChiTest operation computes a $$ \\displaystyle \\chi^{2} $$ statistic for comparing two distributions or a $$ \\displaystyle \\chi^{2} $$ statistic for…"
slug: /commands/statschitest
---

<div className="command-signature">

## <strong>StatsChiTest</strong>  [/NCON=<em>nCon</em> /S/Z] <em>srcWave1</em>, <em>srcWave2</em> {#statschitest}

</div>

The StatsChiTest operation computes a 
$$
\displaystyle \chi^{2}
$$
 statistic for comparing two distributions or a 
$$
\displaystyle \chi^{2}
$$
 statistic for comparing a sample distribution with its expected values. In both cases the comparison is made on a bin-by-bin basis. Output is to the W_StatsChiTest wave in the current data folder or optionally to a table.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/ALZR</span> | Allows zero entries in source waves. If you are using /S zero entries in *srcWave2* are skipped. |
| <span class="table-cell-nowrap">/DEST = *sWave*</span> | Specify the output wave for StatsChiTest.  If you do not specify this flag, the operation stores the output in the wave W_StatsChiTest in the current data folder. |
|  | This flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/FREE</span> | Creates the specified destination wave as a free wave. |
|  | /FREE is allowed only in functions, and only if the destination waves are simple names or wave reference structure fields. |
|  | See [Free Waves](/igorpro/programming/programming.md#free-waves) for more discussion. |
|  | The /FREE flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/NCON = *nCon*</span> | Specifies the number of constraints (0 by default), which reduces the number degrees of freedom and the critical value by *nCon*. |
| <span class="table-cell-nowrap">/S</span> | Sets the calculation mode to a single distribution where *srcWave1* represents an array of binned measurements and *srcWave2* represents the corresponding expected values. |
| <span class="table-cell-nowrap">/T = *k*</span> | Displays results in a table. k specifies the table behavior when it is closed. |
|  |<table class="nested-table"><tbody><tr><td>*k*&nbsp;=0:</td><td>Normal with dialog (default).</td></tr><tr><td>*k*&nbsp;=1:</td><td>Kills with no dialog.</td></tr><tr><td>*k*&nbsp;=2:</td><td>Disables killing.</td></tr></tbody></table>
| <span class="table-cell-nowrap">/Z</span> | Ignores errors. V_flag will be set to -1 for any error and to zero otherwise. |

### *Details* {#details}
The source waves, *srcWave1* and *srcWave2*, must have the same number of points and can be any real numeric data type. Any nonpositive values (including NaN) in either wave removes the entry from consideration in both waves and reduces the degrees of freedom by one. The number degrees of freedom is initially the number of points in *srcWave1*-1-*nCon*. By default it is assumed that *srcWave1* and *srcWave2* represent two distributions of binned data.

When you specify /S, *srcWave1* must consist of binned values of measured data and *srcWave2* must contain the corresponding expected values. The calculation is:

$$
\displaystyle \chi^{2}=\sum_{i=0}^{n-1} \frac{\left(Y_{i}-V_{i}\right)^{2}}{V_{i}} .
$$

Here Y<sub>i</sub> is the sample point from *srcWave1*, V<sub>i</sub> is the expected value of Y<sub>i</sub> based on an assumed distribution (*srcWave2* ), and *n* is the number of points in the each wave. If you do not use /S, it calculates:

$$
\displaystyle \chi^{2}=\sum_{i=0}^{n-1} \frac{\left(Y_{1 i}-Y_{2 i}\right)^{2}}{Y_{1 i}+Y_{2 i}},
$$

where Y<sub>1i</sub> and Y<sub>2i</sub> are taken from *srcWave1* and *srcWave2* respectively.

V_flag will be set to -1 for any error and to zero otherwise.

### *See Also* {#see-also}
[Statistical Analysis](/igorpro/analysis/statistics.md), [StatsContingencyTable](/igorpro/commands/statscontingencytable.md)

### *Demos* {#demos}
[Open Chi-Test Demo.pxp](#igor-pxp/Examples/Statistics/Chi-Test__Demo.pxp)