---
description: "The StatsDunnettTest operation performs the Dunnett test by comparing multiple groups to a control group."
slug: /commands/statsdunnetttest
---

<div className="command-signature">

## <strong>StatsDunnettTest</strong>  [/ALPH=<em>significance</em> /Q/Z/T=<em>k</em> /WSTR=<em>wList</em> /CIDX=<em>controlIndex</em> /SWN/TAIL=<em>tailCode</em> ] [<em>wave1</em>, <em>wave2</em>,... <em>wave100</em> ] {#statsdunnetttest}

</div>

The StatsDunnettTest operation performs the Dunnett test by comparing multiple groups to a control group. Output is to the M_DunnettTestResults wave in the current data folder or optionally to a table. StatsDunnettTest usually follows StatsANOVA1Test.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/ALPH = *val*</span> | Sets the significance level (default *val* =0.05). |
| <span class="table-cell-nowrap">/CIDX = *cIndex*</span> | Specifies the (zero based) index of the input wave corresponding to the control group. The default is zero (the first wave corresponds to the control group). |
| <span class="table-cell-nowrap">/Q</span> | No results printed in the history area. |
| <span class="table-cell-nowrap">/SWN</span> | Creates a text wave, T_DunnettDescriptors, containing wave names corresponding to each row of the comparison table (Save Wave Names). Use /T to append the text wave to the last column./T=*k* Displays results in a table. *k* specifies the table behavior when it is closed. |
|  |<table class="nested-table"><tbody><tr><td>*k*&nbsp;=0:</td><td>Normal with dialog (default).</td></tr><tr><td>*k*&nbsp;=1:</td><td>Kills with no dialog.</td></tr><tr><td>*k*&nbsp;=2:</td><td>Disables killing.</td></tr></tbody></table>
| <span class="table-cell-nowrap">/TAIL = *tc*</span> | Specifies H<sub>0</sub>. |
|  |<table class="nested-table"><tbody><tr><td>*tc*&nbsp;=1:</td><td>One tailed test (µ<sub>c</sub> &lt;= µ<sub>a</sub>)</td></tr><tr><td>*tc*&nbsp;=2:</td><td>One tailed test (µ<sub>c</sub> &gt;= µ<sub>a</sub>)</td></tr><tr><td>*tc*&nbsp;=4:</td><td>Two tailed test (µ<sub>c</sub> = µ<sub>a</sub>) (default)</td></tr></tbody></table>
|  | Code combinations are not allowed. |
| <span class="table-cell-nowrap">/WSTR = *waveListString*</span> |  |
|  | Specifies a string containing a semicolon-separated list of waves that contain sample data. Use waveListString instead of listing each wave after the flags. |
| <span class="table-cell-nowrap">/Z</span> | Ignores errors. V_flag will be set to -1 for any error and to zero otherwise. |

### *Details* {#details}
StatsDunnettTest inputs are two or more 1D numeric waves (one wave for each group of samples). The input waves may contain different number of points, but they must contain two or more valid entries per wave.

For output to a table (using /T), each labelled row represents the results of the test for comparing the means of one group to the control group, and rows are ordered so that all comparisons are computed sequentially starting with the group having the smallest mean. The contents of the labeled columns are:

|  |  |
| --- | --- |
| First: | The difference between the group means |
| Second: | SE (which is computed for possibly unequal number of points) |
| Third: | The q statistic for the pair which may be positive or negative |
| Fourth: | The critical q' value |
| Fifth: | 0 if the conclusion is to reject H<sub>0</sub> or 1 to accept H<sub>0</sub> |
| Sixth: | The *p*-value |

V_flag will be set to -1 for any error and to zero otherwise.

### *See Also* {#see-also}
[Statistical Analysis](/igorpro/analysis/statistics.md), [StatsTukeyTest](/igorpro/commands/statstukeytest.md), [StatsANOVA1Test](/igorpro/commands/statsanova1test.md), [StatsScheffeTest](/igorpro/commands/statsscheffetest.md), [StatsNPMCTest](/igorpro/commands/statsnpmctest.md)

### *Demos* {#demos}
[Open Dunnett-Test Demo.pxp](#igor-pxp/Examples/Statistics/Dunnett-Test__Demo.pxp)