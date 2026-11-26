---
description: "The StatsTukeyTest operation performs multiple comparison Tukey (HSD) test and optionally the Newman-Keuls test."
slug: /commands/statstukeytest
---

<div className="command-signature">

## <strong>StatsTukeyTest</strong>  [/ALPH=<em>val</em> /NK/Q/Z/SWN/T=<em>k</em> /WSTR=<em>wList</em> ] [<em>wave1</em>, <em>wave2</em>,... <em>wave100</em> ] {#statstukeytest}

</div>

The StatsTukeyTest operation performs multiple comparison Tukey (HSD) test and optionally the Newman-Keuls test. Output is to the M_TukeyTestResults wave in the current data folder. StatsTukeyTest usually follows [StatsANOVA1Test](/igorpro/commands/statsanova1test.md).

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/ALPH = *val*</span> | Sets the significance level (default *val* =0.05). |
| <span class="table-cell-nowrap">/DEST = *dstWave*</span> | Specify the destination wave for the Tukey test results.  If you do not use this flag, the results are stored in the wave M_TukeyTestResults in the current data folder. |
|  | This flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/DSTL = *labWave*</span> | Specify the destination text wave for the descriptors of the test results (see /SWN).  If you do not use this flag, the operation saves the text in the wave T_TukeyDescriptors in the current data folder. |
|  | This flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/FREE</span> | Creates the user-specified destination waves as free waves. |
|  | /FREE is allowed only in functions, and only if the destination waves are simple names or wave reference structure fields. |
|  | See [Free Waves](/igorpro/programming/programming.md#free-waves) for more discussion. |
|  | The /FREE flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/NK</span> | Computes the Newman-Keuls test. |
| <span class="table-cell-nowrap">/Q</span> | No results printed in the history area. |
| <span class="table-cell-nowrap">/SWN</span> | Creates a text wave, T_TukeyDescriptors, containing wave names corresponding to each row of the comparison table (Save Wave Names). Use /T to append the text wave to the last column. |
| <span class="table-cell-nowrap">/T = *k*</span> | Displays results in a table. *k* specifies the table behavior when it is closed. |
|  |<table class="nested-table"><tbody><tr><td>*k*&nbsp;=0:</td><td>Normal with dialog (default).</td></tr><tr><td>*k*&nbsp;=1:</td><td>Kills with no dialog.</td></tr><tr><td>*k*&nbsp;=2:</td><td>Disables killing.</td></tr></tbody></table>
| <span class="table-cell-nowrap">/WSTR = *waveListString*</span> |  |
|  | Specifies a string containing a semicolon-separated list of waves that contain sample data. Use *waveListString* instead of listing each wave after the flags. |
| <span class="table-cell-nowrap">/Z</span> | Ignores errors. V_flag will be set to -1 for any error and to zero otherwise. |

### *Details* {#details}
Inputs to StatsTukeyTest are two or more 1D numeric waves (one wave for each group of samples) containing any numbers of points but with at least two or more valid entries.

The contents of the M_TukeyTestResults columns are: the first contains the difference between the group means 
$$
\displaystyle \bar{X}_{i}-\bar{X}_{j}
$$
, the second contains SE (supports unequal number of points), the third contains the q statistic for the pair, and the fourth contains the critical q value, the fifth contains the conclusion with 0 to reject H<sub>0</sub> (µ<sub>i</sub> == µ<sub>j</sub>) or 1 to accept H<sub>0</sub>, with /NK, the sixth contains the *p* values

$$
\displaystyle p=\operatorname{rank}\left[\bar{X}_{i}\right]-\operatorname{rank}\left[\bar{X}_{j}\right]+1,
$$

the seventh contains the critical values, and the eighth contains the Newman-Keuls conclusion (with 0 to reject and 1 to accept H<sub>0</sub>). The order of the rows is such that all possible comparisons are computed sequentially starting with the comparison of the group having the largest mean with the group having the smallest mean.

V_flag will be set to -1 for any error and to zero otherwise.

### *See Also* {#see-also}
[Statistical Analysis](/igorpro/analysis/statistics.md), [StatsANOVA1Test](/igorpro/commands/statsanova1test.md), [StatsScheffeTest](/igorpro/commands/statsscheffetest.md), [StatsDunnettTest](/igorpro/commands/statsdunnetttest.md)

### *Demos* {#demos}
[Open Tukey-Test Demo.pxp](#igor-pxp/Examples/Statistics/Tukey-Test__Demo.pxp)