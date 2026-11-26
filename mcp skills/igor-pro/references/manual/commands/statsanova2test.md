---
description: "The StatsANOVA2Test operation performs a two-factor analysis of variance (ANOVA) on srcWave."
slug: /commands/statsanova2test
---

<div className="command-signature">

## <strong>StatsANOVA2Test</strong>  [/ALPH=<em>significance</em>  /FAKE=<em>num</em>  /MODL=<em>modelNumber</em>  /T=<em>k</em> /Q/Z] <em>srcWave</em> {#statsanova2test}

</div>

The StatsANOVA2Test operation performs a two-factor analysis of variance (ANOVA) on *srcWave*. Output is to the M_ANOVA2Results wave in the current data folder or optionally to a table.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/ALPH = *val*</span> | Sets the significance level (default 0.05). |
| <span class="table-cell-nowrap">/DEST = *destWave*</span> | Specify the output wave for the test.  If you do not specify this flag, the operation stores the data in the wave M_ANOVA2Results in the current data folder. |
|  | This flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/FAKE = *num*</span> | Specifies the number of points in *srcWave*  obtained by  "estimation". num is subtracted from the Total and Error degrees of freedom. |
| <span class="table-cell-nowrap">/FREE</span> | Creates the destination wave as a free wave. |
|  | /FREE is allowed only in functions, and only if the destinationves are simple names or wave reference structure fields. |
|  | See [Free Waves](/igorpro/programming/programming.md#free-waves) for more discussion. |
|  | The /FREE flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/MODL = *model*</span> | Sets the model number. |
|  |<table class="nested-table"><tbody><tr><td>*model*&nbsp;=1:</td><td>Factor A and factor B are fixed (default).</td></tr><tr><td>*model*&nbsp;=2:</td><td>Both factors are random.</td></tr><tr><td>*model*&nbsp;=3:</td><td>Factor A is fixed and factor B is random.</td></tr></tbody></table>
| <span class="table-cell-nowrap">/Q</span> | No results printed in the history area. |
| <span class="table-cell-nowrap">/T = *k*</span> | Displays results in a table. *k*  specifies the table behavior when it is closed. |
|  |<table class="nested-table"><tbody><tr><td>*k*&nbsp;=0:</td><td>Normal with dialog (default).</td></tr><tr><td>*k*&nbsp;=1:</td><td>Kills with no dialog.</td></tr><tr><td>*k*&nbsp;=2:</td><td>Disables killing.</td></tr></tbody></table>
|  | The table is associated with the test, not the data. If you repeat the test, it will update any existing table with the new results. |
| <span class="table-cell-nowrap">/Z</span> | Ignores errors. V_flag will be set to -1 for any error and to zero otherwise. |

### *Details* {#details}
Input to StatsANOVA2Test is the single or double precision 3D srcWave in which the factor A levels are columns, the factor B levels are rows, and the replicates are layers. If srcWave contains dimension labels they will be used to designate the factors in the output.

Ideally, the number of replicates must be equal for each factor and each level. StatsANOVA2Test supports both equal replication and proportional replication. Proportional replication allows for different number of data in each cell with missing data represented as NaN and the number of points in each cell is given by


```igor
Nij=(sum of data in row i)*(sum of data in column j)/number of samples.
```

If you have no replicates (a single datum per cell) use [StatsANOVA2NRTest](/igorpro/commands/statsanova2nrtest.md) instead. If the number of replicates in your data does not satisfy these conditions you may be able to "estimate" additional replicates using various methods. In that case use the /FAKE flag so that the operation can account for the estimated data by reducing the total and error degrees of freedom. /FAKE only accounts for the number of estimates being used. You must provide an appropriate number of estimated values.

The contents of the M_ANOVA2Results output wave columns are: the first contains the sum of the squares (SS) values, the second the degrees of freedom (DF), the third contains the mean square (MS) values, the fourth contains the computed F value for this test, the fifth contains the critical Fc value for the specified alpha and degrees of freedom, and the last contains the conclusion with 0 to reject H<sub>0</sub> or 1 to accept it. In each case H<sub>0</sub> corresponds to the mean level, which is the same for all populations.

V_flag will be set to -1 for any error and to zero otherwise.

### *See Also* {#see-also}
[Statistical Analysis](/igorpro/analysis/statistics.md), [StatsANOVA1Test](/igorpro/commands/statsanova1test.md), [StatsANOVA2NRTest](/igorpro/commands/statsanova2nrtest.md)

### *Demos* {#demos}
[Open ANOVA2 Demo.pxp](#igor-pxp/Examples/Statistics/ANOVA2__Demo.pxp)