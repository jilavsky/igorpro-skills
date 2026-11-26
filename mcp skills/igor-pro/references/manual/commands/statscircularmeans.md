---
description: "The StatsCircularMeans operation calculates the mean of a number of circular means, returning the mean angle (grand mean), the length of the mean vector, and…"
slug: /commands/statscircularmeans
---

<div className="command-signature">

## <strong>StatsCircularMeans</strong>  [/ALPH=<em>significance</em> /CI/Q/Z/T=<em>k</em> ] <em>srcWave</em> {#statscircularmeans}

</div>

The StatsCircularMeans operation calculates the mean of a number of circular means, returning the mean angle (grand mean), the length of the mean vector, and optionally confidence interval around the mean angle. Output is to the history area and to the W_CircularMeans wave in the current data folder.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/ALPH = *val*</span> | Sets the significance level (default 0.05). |
| <span class="table-cell-nowrap">/CI</span> | Calculates the confidence interval (labeled CI_t1 and CI_t2) around the mean angle. |
| <span class="table-cell-nowrap">/DEST = *sWave*</span> | Specify the destination wave for the circular means results.  If you do not use this flag, the operation saves this output in the wave W_CircularMeans in the current data folder. |
|  | This flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/FREE</span> | Creates the user-specified destination wave as a free wave. |
|  | /FREE is allowed only in functions, and only if the destination waves are simple names or wave reference structure fields. |
|  | See [Free Waves](/igorpro/programming/programming.md#free-waves) for more discussion. |
|  | The /FREE flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/NSOA</span> | Performs nonparametric second order analysis according to Moore's version of Rayleigh's test where H<sub>0</sub> corresponds to uniform distribution around the circle. Moore's test ranks entries by the lengths of the mean radii (second column of the input) from smallest (rank 1) to largest (rank *n*) and then computes the statistic: |
|  | $$ R^{\prime}=\sqrt{\frac{\displaystyle \left(\frac{1}{n} \sum_{i=0}^{n-1}(i+1) \cos \left(a_{i}\right)\right)^{2}+\left(\frac{1}{n} \sum_{i=0}^{n-1}(i+1) \sin \left(a_{i}\right)\right)^{2}}{n}}, $$ |
|  | where *a*<sub>i</sub> are the mean angle entries (from column 1) corresponding to vector length rank (*i*+1). The critical value is obtained from Moore's distribution [StatsInvMooreCDF](/igorpro/commands/statsinvmoorecdf.md). |
| <span class="table-cell-nowrap">/PSOA</span> | Perform parametric second order analysis where H<sub>0</sub> corresponds to no mean population direction. It assumes that the second order quantities are from a bivariate normal distribution. If this is not the case, use /NSOA above. The test statistic is: |
|  | $$ \displaystyle F=\frac{k(k-2)}{2}\left[\frac{\bar{X}^{2} S_{y^{2}}-2 \bar{X} \bar{Y} S_{x y}+\bar{Y}^{2} S_{x^{2}}}{S_{x^{2}} S_{y^{2}}-S_{x y}^{2}}\right], $$ |
|  | where |
|  | $$ \begin{array}{l} \bar{X}=\displaystyle\frac{1}{n} \sum_{i=0}^{n-1} X_{i}=\frac{1}{n} \sum_{i=0}^{n-1} r_{i} \cos \left(a_{i}\right), \\ \\ \bar{Y}=\displaystyle\frac{1}{n} \sum_{i=0}^{n-1} Y_{i}=\frac{1}{n} \sum_{i=0}^{n-1} r_{i} \sin \left(a_{i}\right), \\ \\ S_{x^{2}}=\displaystyle\sum_{i=0}^{n-1} X_{i}^{2}-\frac{1}{n}\left(\sum_{i=0}^{n-1} X_{i}\right)^{2}, \\ \\ S_{y^{2}}=\displaystyle\sum_{i=0}^{n-1} Y_{i}^{2}-\frac{1}{n}\left(\sum_{i=0}^{n-1} Y_{i}\right)^{2}, \\ \\ S_{x y}=\displaystyle\sum_{i=0}^{n-1} X_{i} Y_{i}-\frac{1}{n} \sum_{i=0}^{n-1} X_{i} \sum_{i=0}^{n-1} Y_{i} . \end{array} $$ |
|  | Here n is the number of means in srcWave and the critical value is computed from the F distribution, equivalent to executing: |
|  | <code class="igor">Print StatsInvFCDF(1-alpha,2,n-2)</code> |
| <span class="table-cell-nowrap">/Q</span> | No results printed in the history area. |
| <span class="table-cell-nowrap">/T = *k*</span> | Displays results in a table. *k*  specifies the table behavior when it is closed. |
|  |<table class="nested-table"><tbody><tr><td>*k*&nbsp;=0:</td><td>Normal with dialog (default).</td></tr><tr><td>*k*&nbsp;=1:</td><td>Kills with no dialog.</td></tr><tr><td>*k*&nbsp;=2:</td><td>Disables killing.</td></tr></tbody></table>
| <span class="table-cell-nowrap">/Z</span> | Ignores errors. |

### *Details* {#details}
The *srcWave*  input to StatsCircularMeans must be a single or double precision two column wave containing in each row a mean angle (radians) and the length of a mean radius (the first column contains mean angles and the second column contains mean vector lengths). *srcWave*  must not contain any NaNs or INFs. The confidence interval calculation follows the procedure outlined by Batschelet.

V_flag will be set to -1 for any error and to zero otherwise.

### *References* {#references}
Zar, J.H., *Biostatistical Analysis*, 4th ed., 929 pp., Prentice Hall, Englewood Cliffs, New Jersey, 1999.

### *See Also* {#see-also}
[Statistical Analysis](/igorpro/analysis/statistics.md), [StatsCircularMoments](/igorpro/commands/statscircularmoments.md), [StatsInvMooreCDF](/igorpro/commands/statsinvmoorecdf.md), [StatsInvFCDF](/igorpro/commands/statsinvfcdf.md)