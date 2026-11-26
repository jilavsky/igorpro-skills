---
description: "The StatsANOVA2NRTest operation performs a two-factor analysis of variance (ANOVA) on the data that has no replication where there is only a single datum for…"
slug: /commands/statsanova2nrtest
---

<div className="command-signature">

## <strong>StatsANOVA2NRTest</strong>  [/ALPH=<em>significance</em>  /MODL=<em>modelNumber</em>  /Q/Z /T=<em>k</em> ]  <em>srcWave</em> {#statsanova2nrtest}

</div>

The StatsANOVA2NRTest operation performs a two-factor analysis of variance (ANOVA) on the data that has no replication where there is only a single datum for every factor level. srcWave is a 2D wave of any numeric type. Output is to the M_ANOVA2NRResults wave in the current data folder or optionally to a table.

### *Flags* {#flags}

|  |  |  |  |  |
| --- | --- | --- | --- | --- |
| <span class="table-cell-nowrap">/ALPH = *val*</span> | Sets the significance level (default 0.05). |  |  |  |
| <span class="table-cell-nowrap">/DEST = *destWave*</span> | Specify the output wave for the test.  If you do not specify this flag, the operation stores the data in the wave M_ANOVA2NRResults in the current data folder. |  |  |  |
|  | This flag was added in Igor Pro 10.00. |  |  |  |
| <span class="table-cell-nowrap">/FREE</span> | Creates the destination wave as a free wave. |  |  |  |
|  | /FREE is allowed only in functions, and only if the destination waves are simple names or wave reference structure fields. |  |  |  |
|  | See [Free Waves](/igorpro/programming/programming.md#free-waves) for more discussion. |  |  |  |
|  | The /FREE flag was added in Igor Pro 10.00. |  |  |  |
| <span class="table-cell-nowrap">/FOMD</span> | Estimates one missing value. You will also have to use a single or double precision wave for *srcWave*  and designate the single missing value as NaN. The estimated value is printed to the history as well as the bias used to correct the sum of the squares of factor A. |  |  |  |
| <span class="table-cell-nowrap">/INT = *val*</span> | Sets the degree of interactivity. |  |  |  |
|  | *val* =0: | No interaction between the factors (default). |  |  |
|  | *val* =1: | Significant interaction effect between factors. |  |  |
|  | Combination with /MODL determines which factors to test: |  |  |  |
|  | **val** | **Model 1** | **Model 2** | **Model 3** |
|  | **1** |  | A&B | A |
|  | **0** | A&B | A&B | A&B |
|  | As indicated in the table, factor B is not tested for significant interaction under Model 3 and neither factor A nor factor B are tested for Model 1. If you are willing to accept an increase in Type II error you can obtain the relevant values by specifying Model 2. None of the models support a test for interaction A x B. |  |  |  |
| <span class="table-cell-nowrap">/MODL = *model*</span> | Sets the model number. |  |  |  |
|  | *model* =1: | Factor A and factor B are fixed. |  |  |
|  | *model* =2: | Both factors are random. |  |  |
|  | *model* =3: | Factor A is fixed and factor B is random (default). |  |  |
| <span class="table-cell-nowrap">/Q</span> | quiet mode — does not print results in the history. |  |  |  |
| <span class="table-cell-nowrap">/T = *k*</span> | Displays results in a table. *k*  specifies the table behavior when it is closed. |  |  |  |
|  | *k* =0: | Normal with dialog (default). |  |  |
|  | *k* =1: | Kills with no dialog. |  |  |
|  | *k* =2: | Disables killing. |  |  |
|  | The table is associated with the test, not the data. If you repeat the test, it will update any existing table with the new results.. |  |  |  |
| <span class="table-cell-nowrap">/Z</span> | Ignores errors. V_flag will be set to -1 for any error and to zero otherwise. |  |  |  |

### *Details* {#details}
Input to StatsANOVA2NRTest is a 2D wave in which the Factor A corresponds to rows and Factor B corresponds to columns. H<sub>0</sub> provides that there is no difference in the means of the respective populations, i.e., if H<sub>0</sub> is rejected for Factor A but accepted for Factor B that means that there is no difference in the means of the columns but the means of the rows are different.

NaN and INF entries are not supported although you may use a single NaN value in combination with the /FOMD flag. If *srcWave*  contains dimension labels they will be used to designate the two factors in the output.

The contents of the M_ANOVA2NRResults output wave columns are as follows:

|  |  |
| --- | --- |
| Column 0 | Sum of the squares (SS) values |
| Column 1 | Degrees of freedom (DF) |
| Column 2 | Mean square (MS) values |
| Column 3 | Computed F value for this test |
| Column 4 | Critical F value (F<sub>c</sub>) for the specified alpha |
| Column 5 | Conclusion with 0 to reject H<sub>0</sub> or 1 to accept it |

The variable V_flag is set to zero if the operation succeeds or to -1 otherwise.

### *See Also* {#see-also}
[Statistical Analysis](/igorpro/analysis/statistics.md), [StatsANOVA1Test](/igorpro/commands/statsanova1test.md), [StatsANOVA2Test](/igorpro/commands/statsanova2test.md)

### *Demos* {#demos}
[Open ANOVA2NR Demo.pxp](#igor-pxp/Examples/Statistics/ANOVA2NR__Demo.pxp)