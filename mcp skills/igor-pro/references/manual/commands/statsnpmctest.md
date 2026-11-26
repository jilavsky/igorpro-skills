---
description: "The StatsNPMCTest operation performs a number of nonparametric multiple comparison tests."
slug: /commands/statsnpmctest
---

<div className="command-signature">

## <strong>StatsNPMCTest</strong>  [/Q/Z/ALPH=<em>val</em> /SWN/T=<em>k</em> /TAIL=<em>tailCode</em> /WSTR=<em>waveListString</em> /TUK/SNK/DHW/CIDX=<em>controlIndex</em> /CONW=<em>contrastWave</em> /FREE /DSTT=<em>tWave</em> /DSTS=<em>sWave</em> /DSTC=<em>cWave</em> /DSTD=<em>dWave</em> /DSTO=<em>oWave</em> ] [<em>wave1</em>, <em>wave2</em>,... <em>wave100</em> ] {#statsnpmctest}

</div>

The StatsNPMCTest operation performs a number of nonparametric multiple comparison tests. Output waves are saved in the current data folder according to the test(s) performed. Some tests are only appropriate when you have the same number of samples in all groups. StatsNPMCTest usually follows [StatsANOVA1Test](/igorpro/commands/statsanova1test.md) or [StatsKWTest](/igorpro/commands/statskwtest.md).

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/ALPH = *val*</span> | Sets the significance level (default *val* =0.05). |
| <span class="table-cell-nowrap">/CIDX = *controlIndex*</span> |  |
|  | Performs nonparametric multiple comparisons on a control group specified by the zero-based *controlIndex* wave in the input list. Output is to the M_NPCCResults wave in the current data folder or optionally to a table. The output column contents are: the first contains the difference between the rank sums of the control and each of the other waves; the second contains the standard error (SE); the third contains the statistic q, defined as the ratio of the difference in rank sums to SE; the fourth contains the critical value which also depends on the tails specification (see /TAIL); and the fifth contains the conclusion with 0 to reject H0 and 1 to accept it. One version of this test applies when all inputs contain the same number of samples. When that is not the case, it uses the Dunn-Holland-Wolfe approach to compute an appropriate SE and to handle possible ties. |
| <span class="table-cell-nowrap">/CONW = *contrastWave*</span> |  |
|  | Performs a nonparametric multiple contrasts tests. *contrastWave* has one point for each input wave. The *contrastWave* value is 1 to include the corresponding (zero based) input wave in the first group, 2 to include the wave in the second group, or zero to exclude the wave. |
|  | The contrast itself is defined as the difference between the normalized sum of the ranks of the first group and that of the second group. If *contrastWave* ={0,1,1,1,2}, then the contrast is computed as |
|  | $$ \displaystyle \text { contrast: } \frac{1}{3}\left[\mathrm{R}_{\mathrm{n} 1}+\mathrm{R}_{\mathrm{n} 2}+\mathrm{R}_{\mathrm{n} 3}\right]-\mathrm{R}_{\mathrm{n} 4} \text {, } $$ |
|  | where *R*<sub>ni</sub>  is the normalized rank sum of the samples from the corresponding input wave. Note the significance of allowing zeros in the contrast wave because the actual ranking is performed on the pool of all the samples. |
|  | Output is to the M_NPMConResults wave in the current data folder or optionally to a table. The output column contents are: the first is the contrast value; the second is the standard error (SE); the third is the statistic S, which is the ratio of the absolute value of the contrast to SE; the fourth is the critical value (from the $$ \displaystyle \chi^{2} $$approximation); and the fifth is the conclusion with 0 to reject H<sub>0</sub> and 1 indicating acceptance. |
|  | This test supports input waves with different number of samples and can also handle tied ranks. Note that the contrast wave used here is structured differently than for [StatsMultiCorrelationTest](/igorpro/commands/statsmulticorrelationtest.md) for ties in the rank sums. Output is to the M_NPMCDHWResults wave in the current data folder or optionally to a table. The output column contents are: the first contains the difference between the means of the rank sums (rank sums divided by the number of samples in the group), the second contains the standard error (SE), the third contains the DHW statistic Q, the fourth contains the critical value, and the fifth contains the conclusion (0 to reject H<sub>0</sub> and 1 to accept). |
| <span class="table-cell-nowrap">/DSTC = *cWave*</span> |  |
|  | Redirects the comparisons-to-control results matrix, normally created as M_NPCCResults, to *cWave*. Applies only when a control group is specified with /CIDX. When /DSTC is used, the default M_NPCCResults wave is not created. |
| <span class="table-cell-nowrap">/DSTD = *dWave*</span> |  |
|  | Redirects the Dunn-Holland-Wolfe (DHW) results matrix, normally created as M_NPMCDHWResults, to *dWave*. Applies only when the DHW analysis is selected with /DHW. When /DSTD is used, the default M_NPMCDHWResults wave is not created. |
| <span class="table-cell-nowrap">/DSTO = *oWave*</span> |  |
|  | Redirects the multiple-contrasts results matrix, normally created as M_NPMConResults, to *oWave*. Applies only when a contrast wave is supplied with /CONW. When /DSTO is used, the default M_NPMConResults wave is not created. |
| <span class="table-cell-nowrap">/DSTS = *sWave*</span> |  |
|  | Redirects the Student-Newman-Keuls (SNK) results matrix, normally created as M_NPMCSNKResults, to *sWave*. Applies only when the SNK analysis is selected with /SNK. When /DSTS is used, the default M_NPMCSNKResults wave is not created. |
| <span class="table-cell-nowrap">/DSTT = *tWave*</span> |  |
|  | Redirects the Tukey-type (Nemenyi) results matrix, normally created as M_NPMCTukeyResults, to *tWave*. Applies only when the Tukey-type analysis is selected with /TUK. When /DSTT is used, the default M_NPMCTukeyResults wave is not created. |
| <span class="table-cell-nowrap">/FREE</span> | Creates the destination waves specified with /DSTT, /DSTS, /DSTC, /DSTD or /DSTO as free waves (see [Free Waves](/igorpro/programming/programming.md#free-waves)). /FREE is allowed only from within a user function. |
| <span class="table-cell-nowrap">/Q</span> | No results printed in the history area. |
| <span class="table-cell-nowrap">/SWN</span> | Creates a text wave containing wave names corresponding to each row of the comparison table. Depending on your choice of tests, the following waves are created: |
|  |<table class="nested-table"><tbody><tr><td>/CIDX&nbsp;test:</td><td>T_NPCCResultsDescriptors</td></tr><tr><td>/DHW&nbsp;test:</td><td>T_NPMCDHWDescriptors</td></tr><tr><td>/SNK&nbsp;test:</td><td>T_NPMCSNKResultsDescriptors</td></tr><tr><td>/TUK&nbsp;test:</td><td>T_NPMCTukeyDescriptors</td></tr></tbody></table>
| <span class="table-cell-nowrap">/T = *k*</span> | Displays results in a table. *k* specifies the table behavior when it is closed. |
|  |<table class="nested-table"><tbody><tr><td>*k*&nbsp;=0:</td><td>Normal with dialog (default).</td></tr><tr><td>*k*&nbsp;=1:</td><td>Kills with no dialog.</td></tr><tr><td>*k*&nbsp;=2:</td><td>Disables killing.</td></tr></tbody></table>
| <span class="table-cell-nowrap">/TAIL = *tailCode*</span> | Specifies H<sub>0</sub> with /CIDX. |
|  |<table class="nested-table"><tbody><tr><td>*tailCode*&nbsp;=1:</td><td>One tailed test (µ<sub>c</sub> &lt;= µ<sub>a</sub>).</td></tr><tr><td>tc*tailCode*&nbsp;2:</td><td>One tailed test (µ<sub>c</sub> &gt;= µ<sub>a</sub>).</td></tr><tr><td>*tailCode*&nbsp;=4:</td><td>Default; two tailed test (µ<sub>c</sub> = µ<sub>a</sub>).</td></tr></tbody></table>
|  | Code combinations are not allowed. |
| <span class="table-cell-nowrap">/SNK</span> | Performs a nonparametric variation on the Student-Newman-Keuls test where the standard error SE is a function of p (the rank difference). This test requires equal numbers of samples in all groups; use /DHW for unequal sizes. |
|  | Output is to the M_NPMCSNKResults wave in the current data folder. The output column contents are: the first contains the difference between rank sums, the second contains the standard error (SE), the third contains the p value (rank difference), the fourth the statistic, the fifth contains the critical value, and the sixth contains the conclusion (0 to reject H0 and 1 to accept). This test is more sensitive to differences than the Tukey test (/TUK). |
| <span class="table-cell-nowrap">/TUK</span> | Perform a Tukey-type (Nemenyi) multiple comparison test using the difference between the rank sums. This is the default that is performed if you do not specify any of the test flags. This test requires equal numbers of points in all waves; use /DHW for unequal sizes. |
|  | Output is to the M_NPMCTukeyResults wave in the current data folder. The output column contents are: the first contains the difference between the rank sums, the second contains the SE values, the third contains the statistic q, the fourth contains the critical value for this specific alpha and the number of groups; and the last contains a conclusion flag with 0 indicating a rejection of H<sub>0</sub> and 1 indicating acceptance. H<sub>0</sub> postulates that the paired means are the same. |
| <span class="table-cell-nowrap">/WSTR = *waveListString*</span> |  |
|  | Specifies a string containing a semicolon-separated list of waves that contain sample data. Use *waveListString* instead of listing each wave after the flags. |
| <span class="table-cell-nowrap">/Z</span> | Ignores errors. |

### *Details* {#details}
Inputs to StatsNPMCTest are two or more 1D numerical waves (one wave for each group of samples) containing two or more valid entries. The waves must have the same number of points for the use /SNK and /TUK tests, otherwise, for waves of differing lengths you must use the Dunn-Holland-Wolfe test (/DHW).

By default each test writes its output to a wave with a fixed name in the current data folder. The /DSTT, /DSTS, /DSTC, /DSTD, and /DSTO flags redirect these output matrices to waves of your choice (including waves in another data folder), so that existing waves are not overwritten. Each /DSTx flag pairs with the analysis that produces the corresponding matrix; specifying a /DSTx flag without its associated test flag has no effect. A destination wave may not be the same as any of the input data waves or the /CONW contrast wave. Use /FREE to create the destination waves as free waves; /FREE is allowed only from within a user function.

V_flag will be set to zero for no execution errors. Individual tests may fail if, for example, there are different number of samples in the input waves for a test that requires an equal number of points. StatsNPMCTest skips failed tests and V_flag will be a binary combination identifying the failed test(s):

|  |  |
| --- | --- |
| V_flag & 1 | Tukey method failed (/TUK). |
| V_flag & 2 | Student-Newman-Keuls failed (/SNK). |

V_flag will be set to -1 for any other errors.

### *See Also* {#see-also}
[Statistical Analysis](/igorpro/analysis/statistics.md), [StatsANOVA1Test](/igorpro/commands/statsanova1test.md), [StatsKWTest](/igorpro/commands/statskwtest.md)

For multiple comparisons in parametric tests see: [StatsDunnettTest](/igorpro/commands/statsdunnetttest.md) and [StatsScheffeTest](/igorpro/commands/statsscheffetest.md)

### *Demos* {#demos}
[Open NonParametric MultiCompDemo.pxp](#igor-pxp/Examples/Statistics/NonParametric__MultiCompDemo.pxp)