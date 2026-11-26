---
description: "The StatsFriedmanTest operation performs Friedman's test on a randomized block of data."
slug: /commands/statsfriedmantest
---

<div className="command-signature">

## <strong>StatsFriedmanTest</strong>  [/ALPH=<em>significance</em> /RW/T=<em>k</em> /Q/Z/WSTR=<em>wList</em> ]   [<em>wave1</em>,<em>wave2</em>,... <em>wave100</em> ] {#statsfriedmantest}

</div>

The StatsFriedmanTest operation performs Friedman's test on a randomized block of data. It is a nonparametric analysis of data contained in either individual 1D waves or in a single 2D wave. Output is to the M_FriedmanTestResults wave in the current data folder or optionally to a table.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/ALPH = *val*</span> | Sets the significance level (default *val* =0.05). |
| <span class="table-cell-nowrap">/DEST = *destWave*</span> | Specify the output wave for the test results.  If you do not specify this flag, the operation stores the output in the wave M_FriedmanTestResults in the current data folder. |
|  | This flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/FREE</span> | Creates the specified destination wave as a free wave. |
|  | /FREE is allowed only in functions, and only if the destination waves are simple names or wave reference structure fields. |
|  | See [Free Waves](/igorpro/programming/programming.md#free-waves) for more discussion. |
|  | The /FREE flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/Q</span> | No results printed in the history area. |
| <span class="table-cell-nowrap">/RW</span> | Saves the ranking wave M_FriedmanRanks, which contains the rank values corresponding to each input datum. |
| <span class="table-cell-nowrap">/T = *k*</span> | Displays results in a table. *k*  specifies the table behavior when it is closed. |
|  |<table class="nested-table"><tbody><tr><td>*k*&nbsp;=0:</td><td>Normal with dialog (default).</td></tr><tr><td>*k*&nbsp;=1:</td><td>Kills with no dialog.</td></tr><tr><td>*k*&nbsp;=2:</td><td>Disables killing.</td></tr></tbody></table>
|  | The table is associated with the test and not with the data. If you repeat the test, it will update the table with the new results. |
| <span class="table-cell-nowrap">/WSTR = *waveListString*</span> |  |
|  | Specifies a string containing a semicolon-separated list of waves that contain sample data. Use *waveListString*  instead of listing each wave after the flags. |
| <span class="table-cell-nowrap">/Z</span> | Ignores errors. V_flag will be set to -1 for any error and to zero otherwise. |

### *Details* {#details}
The Friedman test ranks the input data on a row-by-row basis, sums the ranks for each column, and computes the Friedman statistic, which is proportional to the sum of the squares of the ranks.

Input waves can be a single 2D wave or a list of 1D numeric waves, which can also be specified in a string list with /WSTR. All 1D waves must have the same number of points. A 2D wave must not contain any NaNs.

The critical value for the Friedman distribution is fairly difficult to compute when the number of rows and columns is large because it requires a number of permutations on the order of (numColumns!)^numRows. A certain range of these critical values are supported by precomputed tables. When the exact critical value is not available you can use one of the two approximations that are always computed: the Chi-squared approximation or the Iman and Davenport approximation, which converts the Friedman statistic is converted to a new value Ff then compares it with critical values from the F distribution using weighted degrees of freedom.

With the /T flag, it displays the results in a table that contains the number of rows, the number of columns, the Friedman statistic, the exact critical value (if available), the Chi-squared approximation, the Iman and Davenport approximation, and the conclusion (1 to accept H<sub>0</sub> and 0 to reject it).

V_flag will be set to -1 for any error and to zero otherwise.

### *References* {#references}
Iman, R.L., and J.M. Davenport, Approximations of the critical region of the Friedman statistic, *Comm. Statist. A9*, 571-595, 1980.

### *See Also* {#see-also}
[Statistical Analysis](/igorpro/analysis/statistics.md), [StatsFriedmanCDF](/igorpro/commands/statsfriedmancdf.md), [StatsInvFriedmanCDF](/igorpro/commands/statsinvfriedmancdf.md)

### *Demos* {#demos}
[Open Friedman-Test Demo.pxp](#igor-pxp/Examples/Statistics/Friedman-Test__Demo.pxp)