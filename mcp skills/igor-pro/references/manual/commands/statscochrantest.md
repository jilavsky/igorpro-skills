---
description: "The StatsCochranTest operation performs Cochran's (Q) test on a randomized block or repeated measures dichotomous data."
slug: /commands/statscochrantest
---

<div className="command-signature">

## <strong>StatsCochranTest</strong>  [/Q/Z/ALPH=<em>significance</em> /T=<em>k</em> /WSTR=<em>wList</em> ]   [<em>wave1</em>,<em>wave2</em>, ... <em>wave100</em> ] {#statscochrantest}

</div>

The StatsCochranTest operation performs Cochran's (Q) test on a randomized block or repeated measures dichotomous data. Output is to the M_CochranTestResults wave in the current data folder or optionally to a table.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/ALPH = *val*</span> | Sets the significance level (default *val* =0.05). |
| <span class="table-cell-nowrap">/DEST = *destWave*</span> | Specify the output wave for the test.  If you do not specify this flag, the operation stores the data in the wave M_CochranTestResults in the current data folder. |
|  | This flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/FREE</span> | Creates the destination wave as a free wave. |
|  | /FREE is allowed only in functions, and only if the destination waves are simple names or wave reference structure fields. |
|  | See [Free Waves](/igorpro/programming/programming.md#free-waves) for more discussion. |
|  | The /FREE flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/Q</span> | No information printed in the history area. |
| <span class="table-cell-nowrap">/T = *k*</span> | Displays results in a table. *k* specifies the table behavior when it is closed. |
|  |<table class="nested-table"><tbody><tr><td>*k*&nbsp;=0:</td><td>Normal with dialog (default).</td></tr><tr><td>*k*&nbsp;=1:</td><td>Kills with no dialog.</td></tr><tr><td>*k*&nbsp;=2:</td><td>Disables killing.</td></tr></tbody></table>
|  | The table is associated with the test and not with the data. If you repeat the test, it will update the table with the new results unless you moved the output wave to a different data folder. If the named table exists but it does not display the output wave from the current data folder, the table is renamed and a new table is created. |
| <span class="table-cell-nowrap">/WSTR = *waveListString*</span> |  |
|  | Specifies a string containing a semicolon-separated list of waves that contain sample data. Use *waveListString* instead of listing each wave after the flags. |
| <span class="table-cell-nowrap">/Z</span> | Ignores errors. V_flag will be set to -1 for any error and to zero otherwise. |

### *Details* {#details}
StatsCochranTest computes Cochran's statistic and compares it to a critical value from a Chi-squared distribution, which depends only of the significance level and the number of groups (columns). The null hypothesis for the test is that all columns represent the same proportion of the effect represented by a non-zero data.

The Chi-square distribution is appropriate when there are at least 4 columns and at least 24 total data points.

Dichotomous data are presumed to consist of two values 0 and 1, thus StatsCochranTest distinguishes only between zero and any nonzero value, which is considered to be 1; it does not allow NaNs or INFs. Input waves can be a single 2D wave or a list of 1D numeric waves, which can also be specified in a string list with /WSTR. In the standard terminology, data rows represent blocks and data columns represent groups. H<sub>0</sub> corresponds to the assumption that all groups have the same proportion of 1's.

With the /T flag, it displays the results in a table that contains the number of rows, the number of columns, the Cochran statistic, the critical value, and the conclusion (1 to accept H<sub>0</sub> and 0 to reject it).

V_flag will be set to -1 for any error and to zero otherwise.

### *See Also* {#see-also}
[Statistical Analysis](/igorpro/analysis/statistics.md), [StatsFriedmanTest](/igorpro/commands/statsfriedmantest.md)

### *Demos* {#demos}
[Open Cochran-Test Demo.pxp](#igor-pxp/Examples/Statistics/Cochran-Test__Demo.pxp)