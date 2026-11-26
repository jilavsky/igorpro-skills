---
description: "The StatsScheffeTest operation performs Scheffe's test for the equality of the means."
slug: /commands/statsscheffetest
---

<div className="command-signature">

## <strong>StatsScheffeTest</strong>  [/ALPH=<em>val</em> /T=<em>k</em> /Q/SWN/Z/WSTR=<em>waveListString</em> /CONW=<em>contrastWave</em> ] [<em>wave1</em>, <em>wave2</em>,... <em>wave100</em> ] {#statsscheffetest}

</div>

The StatsScheffeTest operation performs Scheffe's test for the equality of the means. It supports two basic modes: the default tests all possible combinations of pairs of waves; the second tests a single combination where the precise form of H<sub>0</sub> is determined by the coefficients of a contrast wave (see /CONT). Output is to the M_ScheffeTestResults wave in the current data folder.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/ALPH = *val*</span> | Sets the significance level (default *val* =0.05). |
| <span class="table-cell-nowrap">/CONW = *cWave*</span> | Performs a multiple contrasts test. *cWave* has one point for each input wave. The *cWave* value is 1 to include the corresponding (zero based) input wave in the first group, 2 to include the wave in the second group, or zero to exclude the wave. |
|  | The contrast is defined as the difference between the normalized sum of the ranks of the first group and that of the second group. If *cWave* ={0,1,1,1,2}, then the contrast hypothesis H<sub>0</sub> corresponds to: |
|  | $$ \displaystyle \frac{\bar{X}_{1}+\bar{X}_{2}+\bar{X}_{3}}{3}-\bar{X}_{4}=0 $$ |
|  | For each pair of waves $$ \displaystyle (i, j) $$ with $$ \displaystyle i \neq j $$, it computes |
|  | $$ S E_{i j}=\sqrt{s^{2}\left(\frac{1}{n_{j}}+\frac{1}{n_{i}}\right)}, \quad s^{2}=\sum_{i=1}^{W} \sum_{j=0}^{n_{j}-1} X_{j}^{2}-\sum_{i=1}^{W} \frac{\displaystyle \left(\sum_{j=0}^{n_{j}-1} X_{j}\right)^{2}}{n_{j}}, $$ |
|  | the statistic |
|  | $$ S=\frac{\displaystyle \left\|\sum_{i=0}^{n-1} c_{i} \bar{X}_{i}\right\|}{S E}, $$ |
|  | the critical value, and a result field which is set to 1 if H<sub>0</sub> should be accepted or 0 if it should be rejected. *W* is the total number of waves, *n*<sub>i</sub>  and $$ \displaystyle \bar{X}_{i} $$ are respectively the number of data points and the average of wave *i*. |
| <span class="table-cell-nowrap">/DEST = *dstWave*</span> | Specify the destination wave for the Scheffe test results.  If you do not use this flag, the results are stored in the wave M_ScheffeTestResults in the current data folder. |
|  | This flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/DSTL = *labWave*</span> | Specify the destination text wave for the descriptors of the test results (see /SWN).  If you do not use this flag, the operation saves the text in the wave T_ScheffeDescriptors in the current data folder. |
|  | This flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/FREE</span> | Creates the user-specified destination waves as free waves. |
|  | /FREE is allowed only in functions, and only if the destination waves are simple names or wave reference structure fields. |
|  | See [Free Waves](/igorpro/programming/programming.md#free-waves) for more discussion. |
|  | The /FREE flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/Q</span> | No results printed in the history area. |
| <span class="table-cell-nowrap">/SWN</span> | Creates a text wave, T_ScheffeDescriptors, containing wave names corresponding to each row of the comparison table (Save Wave Names). Use /T to append the text wave to the last column. |
| <span class="table-cell-nowrap">/T = *k*</span> | Displays results in a table. *k* specifies the table behavior when it is closed. |
|  |<table class="nested-table"><tbody><tr><td>*k*&nbsp;=0:</td><td>Normal with dialog (default).</td></tr><tr><td>*k*&nbsp;=1:</td><td>Kills with no dialog.</td></tr><tr><td>*k*&nbsp;=2:</td><td>Disables killing.</td></tr></tbody></table>
|  | The table is associated with the test, not the data. If you repeat the test, it will update any existing table with the new results. |
| <span class="table-cell-nowrap">/WSTR = *waveListString*</span> |  |
|  | Specifies a string containing a semicolon-separated list of waves that contain sample data. Use *waveListString* instead of listing each wave after the flags. |
| <span class="table-cell-nowrap">/Z</span> | Ignores errors. V_flag will be set to -1 for any error and to zero otherwise. |

### *Details* {#details}
The default of StatsScheffeTest (also known as the S test) tests the hypotheses of equality of means for each possible pair of samples. It is not as powerful as Tukey's test ([StatsTukeyTest](/igorpro/commands/statstukeytest.md)) and is more useful for hypotheses formulated as multiple contrasts (see /CONT).

### *References* {#references}
See, in particular, Chapter 11 of:

Zar, J.H., *Biostatistical Analysis*, 4th ed., 929 pp., Prentice Hall, Englewood Cliffs, New Jersey, 1999.

### *See Also* {#see-also}
[Statistical Analysis](/igorpro/analysis/statistics.md), [StatsANOVA1Test](/igorpro/commands/statsanova1test.md), [StatsDunnettTest](/igorpro/commands/statsdunnetttest.md), [StatsTukeyTest](/igorpro/commands/statstukeytest.md)

### *Demos* {#demos}
[Open Scheffe-Test Demo.pxp](#igor-pxp/Examples/Statistics/Scheffe-Test__Demo.pxp)