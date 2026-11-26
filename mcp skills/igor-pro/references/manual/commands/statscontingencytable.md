---
description: "The StatsContingencyTable operation performs contingency table analysis on 2D and 3D tables."
slug: /commands/statscontingencytable
---

<div className="command-signature">

## <strong>StatsContingencyTable</strong>  [/ALPH=<em>significance</em> /COR=<em>mode</em> /FEXT={<em>row</em>, <em>col</em>}/HTRG/LLIK/Q/Z /T=<em>k</em> ] <em>srcWave</em> {#statscontingencytable}

</div>

The StatsContingencyTable operation performs contingency table analysis on 2D and 3D tables. Output is to the W_ContingencyTableResults wave in the current data folder or optionally to a table or the history area.

### *Flags* {#flags}

|  |  |  |
| --- | --- | --- |
| <span class="table-cell-nowrap">/ALPH = *val*</span> | Sets the significance level (default *val* =0.05). |  |
| <span class="table-cell-nowrap">/COR = *mode*</span> | Sets the correction type for 2x2 tables. By default there is no correction. Use *mode* =1 for Yates and *mode* =2 for Haber correction. |  |
| <span class="table-cell-nowrap">/DEST = *ctWave*</span> | Specify the destination wave for the results of contingency table analysis.  If you do not use this flag, the operation saves the output in the wave W_ContingencyTableResults in the current data folder. |  |
|  | This flag was added in Igor Pro 10.00. |  |
| <span class="table-cell-nowrap">/FEXT = {*row*, *col*}</span> |  |  |
|  | Computes Fisher's Exact P-value with 2x2 contingency tables. row and col are zero-based indices of the table entry where it computes the probability of getting the results in the table or more extreme values. Without the /Q flag, it prints the probabilities of each individual table in the history. |  |
|  | Given the contingency table: |  |
|  |  |<table class="nested-table"><tbody><tr><td>**Succeeded**</td><td>**Failed**</td></tr></tbody></table>
|  | **Group1** |<table class="nested-table"><tbody><tr><td>11</td><td>8</td></tr></tbody></table>
|  | **Group2** |<table class="nested-table"><tbody><tr><td>4</td><td>9</td></tr></tbody></table>
|  | Example 1: When you use /FEXT={0,0} the P-value represents the sum of the probabilities of the first group having in the Succeeded column 11 or more extreme values, i.e., 12, 13, 14, and 15. In each case the remaining table elements are adjusted so that row and column sums remain constant. |  |
|  | Example 2: When you needed to evaluate the sum of the probabilities of Group2 having 4 counts or less in the Succeeded column, then the appropriate flag is /FEXT={1,1}, which effectively computes the equivalent of having 9, 10, 11, 12, and 13 Failed counts. In each case it computes the upper, the lower, and the two-tail probabilities. |  |
| <span class="table-cell-nowrap">/FREE</span> | Creates the user-specified destination wave as a free wave. |  |
|  | /FREE is allowed only in functions, and only if the destination waves are simple names or wave reference structure fields. |  |
|  | See [Free Waves](/igorpro/programming/programming.md#free-waves) for more discussion. |  |
|  | The /FREE flag was added in Igor Pro 10.00. |  |
| <span class="table-cell-nowrap">/HTRG</span> | Tests for heterogeneity between tables stored as layers of 3D wave. |  |
| <span class="table-cell-nowrap">/LLIK</span> | Computes log likelihood statistic. |  |
| <span class="table-cell-nowrap">/Q</span> | No results printed in the history area. |  |
| <span class="table-cell-nowrap">/T = *k*</span> | Displays results in a table. *k* specifies the table behavior when it is closed. |  |
|  | *k* =0: | Normal with dialog (default). |
|  | *k* =1: | Kills with no dialog. |
|  | *k* =2: | Disables killing. |
|  | The table is associated with the test and not with the data. If you repeat the test, it will update the table with the new results unless you moved the output wave to a different data folder. If the named table exists but it does not display the output wave from the current data folder, the table is renamed and a new table is created. |  |
| <span class="table-cell-nowrap">/Z</span> | Ignores errors. V_flag will be set to -1 for any error and to zero otherwise. |  |

### *Details* {#details}
StatsContingencyTable supports 2D waves representing single contingency tables or 3D waves representing multiple 2D tables (where each table is a layer) or a single 3D table. Each entry in the wave must contain a frequency value and must be a positive number; it does not support 0's, NaNs, or INFs. In the special case of 2x2 tables, use the /COR flag to compute the statistic using either the Yates or Haber corrections. Except for the heterogeneity option you can also compute the log likelihood statistic. In all the tests, H<sub>0</sub> corresponds to independence between the tested variables.

For 3D tables StatsContingencyTable provides Chi-squared, degrees of freedom, the critical value, and optionally the log likelihood G statistic (/LLIK flag) for each of the following cases:


1.	Mutual independence by testing if all three variables are independent of each other.


2.	Partial dependence (rows) by testing if rows independent of columns and layers.


3.	Partial dependence (columns) by testing if columns independent of rows and layers.


4.	Partial dependence (layers) by testing if layers independent of rows and columns.

In each case you should compare the statistic with the critical value and reject H<sub>0</sub> if the statistic exceeds or equals the critical value.

You should examine the table entries to determine if the Chi-square statistic is appropriate (if the frequency is smaller than 6 for /ALPH=0.05 you should consider computing the Fisher exact test).

V_flag will be set to -1 for any error and to zero otherwise.

### *See Also* {#see-also}
[Statistical Analysis](/igorpro/analysis/statistics.md), [StatsInvChiCDF](/igorpro/commands/statsinvchicdf.md)

### *Demos* {#demos}
[Open Contingency Table Demo.pxp](#igor-pxp/Examples/Statistics/Contingency__Table__Demo.pxp)