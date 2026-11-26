---
description: "The StatsLinearCorrelationTest operation performs correlation tests on waveA and waveB, which must be real valued numeric waves and must have the same number…"
slug: /commands/statslinearcorrelationtest
---

<div className="command-signature">

## <strong>StatsLinearCorrelationTest</strong>  [/ALPH=<em>alpha</em>  /T=<em>k</em> /RHO=<em>rhoValue</em> /Q/Z] <em>waveA</em>, <em>waveB</em> {#statslinearcorrelationtest}

</div>

The StatsLinearCorrelationTest operation performs correlation tests on *waveA*  and *waveB*, which must be real valued numeric waves and must have the same number of points. Output is to the W_StatsLinearCorrelationTest wave in the current data folder or optionally to a table.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/ALPH = *val*</span> | Sets the significance level (default *val* =0.05). |
| <span class="table-cell-nowrap">/CI</span> | computes confidence intervals for the correlation coefficient. |
| <span class="table-cell-nowrap">/DEST = *dstWave*</span> | Specify the destination wave for the correlation test results.  If you do not specify this flag, the results are stored in the wave W_StatsLinearCorrelationTest in the current data folder. |
|  | This flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/FREE</span> | Creates the user-specified destination wave as a free wave. |
|  | /FREE is allowed only in functions, and only if the destination waves are simple names or wave reference structure fields. |
|  | See [Free Waves](/igorpro/programming/programming.md#free-waves) for more discussion. |
|  | The /FREE flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/Q</span> | No results printed in the history area. |
| <span class="table-cell-nowrap">/RHO = *rhoValue*</span> | Tests hypothesis that the correlation has a nonzero value \|ρ\|<=1. |
| <span class="table-cell-nowrap">/T = *k*</span> | Displays results in a table. *k*  specifies the table behavior when it is closed. |
|  |<table class="nested-table"><tbody><tr><td>*k*&nbsp;=0:</td><td>Normal with dialog (default).</td></tr><tr><td>*k*&nbsp;=1:</td><td>Kills with no dialog.</td></tr><tr><td>*k*&nbsp;=2:</td><td>Disables killing.</td></tr></tbody></table>
| <span class="table-cell-nowrap">/Z</span> | Ignores errors. |

### *Details* {#details}
The linear correlation tests start by computing the linear correlation coefficient for the *n*  elements of both waves:

$$
r=\frac{\displaystyle \sum_{i=1}^{n} X_{i} Y_{i}-\frac{1}{n} \sum_{i=1}^{n} X_{i} \sum_{i=1}^{n} Y_{i}}{\displaystyle \sqrt{\left(\sum_{i=1}^{n} X_{i}^{2}-\frac{1}{n}\left(\sum_{i=1}^{n} X_{i}\right)^{2}\right)\left(\sum_{i=1}^{n} Y_{i}^{2}-\frac{1}{n}\left(\sum_{i=1}^{n} Y_{i}\right)^{2}\right)}}
$$
*.*



Next it computes the standard error of the correlation coefficient

$$
\displaystyle s r=\sqrt{\frac{1-r^{2}}{n-2}}
$$
*.*

The basic test is for hypothesis H<sub>0</sub>: the correlation coefficient is zero, in which case t and F statistics are applicable. It computes the statistics:

$$
\displaystyle t=r / s r
$$

and

$$
\displaystyle F=(1+|r|) /(1-|r|)
$$
,

and then the critical values for one and two tailed hypotheses (designated by *t*<sub>c1</sub>, *t*<sub>c2</sub>, *F*<sub>c1</sub>, and *F*<sub>c2</sub>  respectively). Critical value for *r*  are computed using

$$
\displaystyle \mathrm{rc}_{\mathrm{i}}=\sqrt{\frac{t_{c}^{2}}{t_{c}^{2}+n}}
$$
,

where *i*  takes the values 1 or 2 for one and two tailed hypotheses. Finally, the operation computes the power of the test at the alpha significance level for both one and two tails (Power1 and Power2).

If you use /RHO it uses the Fisher transformation to compute

$$
\displaystyle \text { Fisher } \mathrm{Z}=\frac{1}{2} \ln \left(\frac{1+r}{1-r}\right)
$$
,

$$
\displaystyle \text { zeta }=\frac{1}{2} \ln \left(\frac{1+\rho}{1-\rho}\right)
$$
,

the standard error approximation

$$
\displaystyle \text { sigmaZ }=\sqrt{1 /(n-3)}
$$
,

$$
\displaystyle \text { Zstatistic=(FisherZ-zeta)/sigmaZ }
$$
,

and the critical values from the normal distribution *Z*<sub>ci</sub>.

The confidence intervals are calculated differently depending on the hypothesis for the value of the correlation coefficient. If /RHO is not used the confidence intervals are computed using the critical value *F*<sub>c2</sub>, otherwise they are computed using the critical *Z*<sub>c2 </sub> and sigmaZ.

### *References* {#references}
See, in particular, Chapter 18 of:

Zar, J.H., *Biostatistical Analysis*, 4th ed., 929 pp., Prentice Hall, Englewood Cliffs, New Jersey, 1999.

### *See Also* {#see-also}
[Statistical Analysis](/igorpro/analysis/statistics.md), [StatsCircularCorrelationTest](/igorpro/commands/statscircularcorrelationtest.md), [StatsMultiCorrelationTest](/igorpro/commands/statsmulticorrelationtest.md), [StatsRankCorrelationTest](/igorpro/commands/statsrankcorrelationtest.md)

### *Demos* {#demos}
[Open Linear Correlation Demo.pxp](#igor-pxp/Examples/Statistics/Linear__Correlation__Demo.pxp)