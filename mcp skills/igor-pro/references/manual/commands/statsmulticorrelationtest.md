---
description: "The StatsMultiCorrelationTest operation performs various tests on multiple correlation coefficients."
slug: /commands/statsmulticorrelationtest
---

<div className="command-signature">

## <strong>StatsMultiCorrelationTest</strong>  [/ALPH=<em>alpha</em>  /T=<em>k</em> /Z/Q/TUK/CON={<em>controlRow</em>, <em>tails</em> }/CONT=<em>contrastWave</em> ] <em>corrWave</em>, <em>sizeWave</em> {#statsmulticorrelationtest}

</div>

The StatsMultiCorrelationTest operation performs various tests on multiple correlation coefficients. Inputs are two 1D waves: *corrWave*, containing correlation coefficients, and *sizeWave*, containing the size (number of elements) of the corresponding samples. Although you can do all the tests at the same time, it rarely makes sense to do so.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/ALPH = *val*</span> | Sets the significance level (default *val* =0.05). |
| <span class="table-cell-nowrap">/CDFF = *func*</span> | Specifies a user function expressing the cumulative distribution function. See Details. |
| <span class="table-cell-nowrap">/CON = {*controlRow*,*tails* }</span> |  |
|  | Performs a multiple comparison test using the *controlRow* element of *corrWave* as a control. It is one- or two-tailed test according to the tails parameter. Output is to the M_ControlCorrTestResults wave in the current data folder. |
| <span class="table-cell-nowrap">/CONT = *cWave*</span> | Performs a multiple contrasts test on the correlation coefficients. The contrasts wave, *cWave*, contains the contrast factor, *c*<sub>i</sub>, entry for each of the *n*  correlation coefficients *r*<sub>i</sub>  in *corrWave*, and satisfying the condition that the sum of the entries in *cWave* is zero. H<sub>0</sub> corresponds to |
|  | $$ \displaystyle \sum_{i=0}^{n-1} c_{i} r_{i}=0 . $$ |
|  | The test statistic *S* is |
|  | $$ \displaystyle S=\left\|\sum_{i=0}^{n-1} c_{i} z_{i}\right\| / \sqrt{\frac{c_{i}^{2}}{n_{i}-3}} $$ |
|  | where *z*<sub>i</sub> is the Fisher z transform of the correlation coefficient *r*<sub>i </sub>: |
|  | $$ \displaystyle z_{i}=\frac{1}{2} \ln \left(\frac{1+r_{i}}{1-r_{i}}\right) . $$ |
|  | It produces the SE value, the contrast statistic S, and the critical value, which are labeled ContrastSE, ContrastS, and Contrast_Critical, respectively, in the W_StatsMultiCorrelationTest wave. |
| <span class="table-cell-nowrap">/DEST = *dstWave*</span> | Specify the destination wave for the correlation test results.  If you do not specify this flag, the results are stored in the wave W_StatsMultiCorrelationTest in the current data folder. |
|  | This flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/FREE</span> | Creates the user-specified destination wave as a free wave. |
|  | /FREE is allowed only in functions, and only if the destination waves are simple names or wave reference structure fields. |
|  | See [Free Waves](/igorpro/programming/programming.md#free-waves) for more discussion. |
|  | The /FREE flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/Q</span> | No results printed in the history area. |
| <span class="table-cell-nowrap">/T = *k*</span> | Displays results in a table. *k* specifies the table behavior when it is closed. |
|  |<table class="nested-table"><tbody><tr><td>*k*&nbsp;=0:</td><td>Normal with dialog (default).</td></tr><tr><td>*k*&nbsp;=1:</td><td>Kills with no dialog.</td></tr><tr><td>*k*&nbsp;=2:</td><td>Disables killing.</td></tr></tbody></table>
| <span class="table-cell-nowrap">/TUK</span> | Performs a Tukey-type multi comparison testing between the correlation coefficients by comparing every possible combination of pairs of correlation coefficients, computing the difference in their z-transforms, the SE, and the *q* statistic: |
|  | $$ q=\frac{\left\|z_{j}-z_{i}\right\|}{\sqrt{\frac{1}{2}\left(\displaystyle \frac{1}{n_{i}-3}+\frac{1}{n_{j}-3}\right)}} . $$ |
|  | The critical value is computed from the *q* CDF ([StatsInvQCDF](/igorpro/commands/statsinvqcdf.md)) with degrees of freedom numWaves and infinity. Output is to the M_TukeyCorrTestResults wave in the current data folder or optionally to a table. |
| <span class="table-cell-nowrap">/Z</span> | Ignores errors. V_flag will be set to -1 for any error and to zero otherwise. |

### *Details* {#details}
Without any flags, StatsMultiCorrelationTest computes 
$$
\displaystyle \chi^{2}
$$
for the correlation coefficients and compares it with the critical value.

$$
\chi^{2}=\sum_{i=0}^{n-1} z_{i}^{2}\left(n_{i}-3\right)-\frac{\displaystyle\left(\sum_{i=0}^{n-1} z_{i}\left(n_{i}-3\right)\right)^{2}}{\displaystyle\sum_{i=0}^{n-1}\left(n_{i}-3\right)},
$$

where *z*<sub>i</sub>  is the Fisher's z transform of the correlation coefficients and *n*<sub>i</sub><sub> </sub> is the corresponding sample size. It computes the common correlation coefficient rw and its transform zw.

$$
z_{w}=\frac{\displaystyle \sum_{i=0}^{n-1} z_{i}\left(n_{i}-3\right)}{\displaystyle \sum_{i=0}^{n-1}\left(n_{i}-3\right)}
$$

These values are calculated even when not appropriate, such as when 
$$
\displaystyle \chi^{2}
$$
exceeds the critical value and H<sub>0</sub> (all samples came from populations of identical correlation coefficients) is rejected.

The operation also computes ChiSquaredP (due to S.R. Paul), a different variant of  
$$
\displaystyle \chi^{2}
$$
that is corrected for bias and should be compared with the same critical value. Output is to the W_StatsMultiCorrelationTest wave in the current data folder or optionally to a table.

### *References* {#references}
See, in particular, Chapters 19 and 11 of:

Zar, J.H., *Biostatistical Analysis*, 4th ed., 929 pp., Prentice Hall, Englewood Cliffs, New Jersey, 1999.

### *See Also* {#see-also}
[Statistical Analysis](/igorpro/analysis/statistics.md), [StatsLinearCorrelationTest](/igorpro/commands/statslinearcorrelationtest.md), [StatsCircularCorrelationTest](/igorpro/commands/statscircularcorrelationtest.md), [StatsDunnettTest](/igorpro/commands/statsdunnetttest.md), [StatsTukeyTest](/igorpro/commands/statstukeytest.md), [StatsInvQCDF](/igorpro/commands/statsinvqcdf.md), [StatsScheffeTest](/igorpro/commands/statsscheffetest.md)

### *Demos* {#demos}
[Open Multi-Correlation Demo.pxp](#igor-pxp/Examples/Statistics/Multi-Correlation__Demo.pxp)