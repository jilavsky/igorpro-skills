---
description: "The StatsRankCorrelationTest operation performs Spearman's rank correlation test on waveA and waveB, 1D waves containing the same number of points."
slug: /commands/statsrankcorrelationtest
---

<div className="command-signature">

## <strong>StatsRankCorrelationTest</strong>  [/ALPH=<em>alpha</em> /P=<em>method</em> /Q /T=<em>k</em> /Z] <em>waveA</em>, <em>waveB</em> {#statsrankcorrelationtest}

</div>

The StatsRankCorrelationTest operation performs Spearman's rank correlation test on *waveA* and *waveB*, 1D waves containing the same number of points. Output is to the W_StatsRankCorrelationTest wave in the current data folder.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/ALPH = *val*</span> | Sets the significance level (default *val* =0.05). |
| <span class="table-cell-nowrap">/P = *method*</span> | Controls the computation of the P-value. |
|  | The /P flag was added in Igor Pro 9.00. |
|  |<table class="nested-table"><tbody><tr><td>*method*=0:</td><td>If the number of data points is less than or equal to 6 then an exact calculation is made. This is the default if /P is omitted.</td></tr><tr><td>*method*=1:</td><td>The P-value is computed using the Edgeworth approximation. The P-value reported corresponds to a two tails calculation.</td></tr><tr><td>*method*=2:</td><td>The P-value is computed using the Student-T approximation. This is appropriate when the number of data points is large.</td></tr></tbody></table>
| <span class="table-cell-nowrap">/Q</span> | No results printed in the history area. |
| <span class="table-cell-nowrap">/T = *k*</span> | Displays results in a table. *k* specifies the table behavior when it is closed. |
|  |<table class="nested-table"><tbody><tr><td>*k*&nbsp;=0:</td><td>Normal with dialog (default).</td></tr><tr><td>*k*&nbsp;=1:</td><td>Kills with no dialog.</td></tr><tr><td>*k*&nbsp;=2:</td><td>Disables killing.</td></tr></tbody></table>
| <span class="table-cell-nowrap">/Z</span> | Ignores errors. |

### *Details* {#details}
StatsRankCorrelationTest ranks *waveA* and *waveB* and then computes the sum of the squared differences of ranks for all rows. Ties are assigned an average rank and the corrected Spearman rank correlation coefficient is computed with ties. It reports the sum of the squared ranks (sumDi2), the sums of the ties coefficients (sumTx and sumTy respectively), the Spearman rank correlation coefficient (in the range [-1,1]), and the critical value. H<sub>0</sub> corresponds to zero correlation against the alternative of nonzero correlation. The critical value is usually lower than the one in published tables. When the first derivative of the CDF is discontinuous, tables tend to use a more conservative value by choosing the next transition of the CDF as the critical value. StatsRankCorrelationTest is not as powerful as [StatsLinearCorrelationTest](/igorpro/commands/statslinearcorrelationtest.md).

### *See Also* {#see-also}
[Statistical Analysis](/igorpro/analysis/statistics.md), [StatsLinearCorrelationTest](/igorpro/commands/statslinearcorrelationtest.md), [StatsCircularCorrelationTest](/igorpro/commands/statscircularcorrelationtest.md), [StatsKendallTauTest](/igorpro/commands/statskendalltautest.md), [StatsSpearmanRhoCDF](/igorpro/commands/statsspearmanrhocdf.md), [StatsInvSpearmanCDF](/igorpro/commands/statsinvspearmancdf.md)

### *Demos* {#demos}
[Open Spearman Rank Demo.pxp](#igor-pxp/Examples/Statistics/Spearman__Rank__Demo.pxp)