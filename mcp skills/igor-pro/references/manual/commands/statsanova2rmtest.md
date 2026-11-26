---
description: "The StatsANOVA2RMTest operation performs analysis of variance (ANOVA) on srcWave where replicates consist of multiple measurements on the same subject…"
slug: /commands/statsanova2rmtest
---

<div className="command-signature">

## <strong>StatsANOVA2RMTest</strong>  [/ALPH=<em>significance</em> /Q/Z/T=<em>k</em> ]  <em>srcWave</em> {#statsanova2rmtest}

</div>

The StatsANOVA2RMTest operation performs analysis of variance (ANOVA) on *srcWave* where replicates consist of multiple measurements on the same subject (repeated measures). *srcWave* is a 2D wave of any numeric type. Output is to the M_ANOVA2RMResults wave in the current data folder or optionally to a table.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/ALPH = *val*</span> | Sets the significance level (default 0.05). |
| <span class="table-cell-nowrap">/DEST = *destWave*</span> | Specify the output wave for the test.  If you do not specify this flag, the operation stores the data in the wave M_ANOVA2RMResults in the current data folder. |
|  | This flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/FREE</span> | Creates the destination wave as a free wave. |
|  | /FREE is allowed only in functions, and only if the destination waves are simple names or wave reference structure fields. |
|  | See [Free Waves](/igorpro/programming/programming.md#free-waves) for more discussion. |
|  | The /FREE flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/Q</span> | No results printed in the history area. |
| <span class="table-cell-nowrap">/T = *k*</span> | Displays results in a table. *k* specifies the table behavior when it is closed. |
|  |<table class="nested-table"><tbody><tr><td>*k*&nbsp;=0:</td><td>Normal with dialog (default).</td></tr><tr><td>*k*&nbsp;=1:</td><td>Kills with no dialog.</td></tr><tr><td>*k*&nbsp;=2:</td><td>Disables killing.</td></tr></tbody></table>
|  | The table is associated with the test, not the data. If you repeat the test, it will update any existing table with the new results. |
| <span class="table-cell-nowrap">/Z</span> | Ignores errors. V_flag will be set to -1 for any error and to zero otherwise. |

### *Details* {#details}
Input to StatsANOVA2RMTest is the 2D *srcWave* in which the factor A (Groups) are columns and the different subjects are rows. It does not support NaNs or INFs.

The contents of the M_ANOVA2RMResults output wave columns are: the first contains the sum of the squares (SS) values, the second contains the degrees of freedom (DF), the third contains the mean square (MS) values, the fourth contains the single F value for this test, the fifth contains the critical F value for the specified alpha and degrees of freedom, and the last column contains the conclusion with 0 to reject H<sub>0</sub> or 1 to accept it. In each case H<sub>0</sub> corresponds the mean level, which is the same for all subjects.

V_flag will be set to -1 for any error and to zero otherwise.

### *See Also* {#see-also}
[Statistical Analysis](/igorpro/analysis/statistics.md), [StatsANOVA2NRTest](/igorpro/commands/statsanova2nrtest.md), [StatsANOVA2Test](/igorpro/commands/statsanova2test.md)

### *Demos* {#demos}
[Open ANOVA2RM Demo.pxp](#igor-pxp/Examples/Statistics/ANOVA2RM__Demo.pxp)