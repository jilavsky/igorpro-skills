---
description: "The StatsFTest operation performs the F-test on the two distributions in wave1 and wave2, which can be any real numeric type, must contain at least two data…"
slug: /commands/statsftest
---

<div className="command-signature">

## <strong>StatsFTest</strong>  [/ALPH=<em>significance</em> /TAIL=<em>tc</em> /T=<em>km</em> /Q/Z] <em>wave1</em>, <em>wave2</em> {#statsftest}

</div>

The StatsFTest operation performs the F-test on the two distributions in wave1 and wave2, which can be any real numeric type, must contain at least two data points each, and can have an arbitrary number of dimensions. Output is to the W_StatsFTest wave in the current data folder or optionally to a table.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/ALPH = *val*</span> | Sets the significance level (default *val* =0.05). |
| <span class="table-cell-nowrap">/TAIL = *tc*</span> | Specifies the tail tested. |
|  |<table class="nested-table"><tbody><tr><td>*tc*&nbsp;=1:</td><td>Lower one-tail test with H<sub>a</sub>: sigma1&gt;sigma2.</td></tr><tr><td>*tc*&nbsp;=2:</td><td>Upper one-tail test with H<sub>a</sub>: sigma1&lt;sigma2.</td></tr><tr><td>*tc*&nbsp;=4:</td><td>Default; the null hypothesis H<sub>0</sub>: sigma1=sigma2 with H<sub>a</sub>: sigma1!=sigma2.</td></tr></tbody></table>
| <span class="table-cell-nowrap">/Q</span> | No results printed in the history area. |
| <span class="table-cell-nowrap">/T = *k*</span> | Displays results in a table. *k* specifies the table behavior when it is closed. |
|  |<table class="nested-table"><tbody><tr><td>*k*&nbsp;=0:</td><td>Normal with dialog (default).</td></tr><tr><td>*k*&nbsp;=1:</td><td>Kills with no dialog.</td></tr><tr><td>*k*&nbsp;=2:</td><td>Disables killing.</td></tr></tbody></table>
| <span class="table-cell-nowrap">/Z</span> | Ignores errors. V_flag will be set to -1 for any error and to zero otherwise. |

### *Details* {#details}
The F statistic is the ratio of the variance of wave1 to the variance of wave2. We assume the waves have equal wave variances and that H<sub>0</sub> is sigma1=sigma2. For the upper one-tail test we reject H<sub>0</sub> if F is greater than the upper critical value or if F is smaller than the lower critical value in the lower one-tail test. In the two-tailed test we reject H<sub>0</sub> if F is either greater than the upper critical value or smaller than the lower critical value. The critical values are computed by numerically solving for the argument at which the cumulative distribution function (CDF) equals the appropriate values for the tests. The CDF is given by

$$
\displaystyle F\left(x, n_{1}, n_{2}\right)=1-{betai}\left(\frac{n_{2}}{2}, \frac{n_{1}}{2}, \frac{n_{2}}{n_{2}+n_{1} x}\right),
$$

where the degrees of freedom *n*<sub>1</sub> and *n*<sub>2</sub> equal the number of valid (non-NaN) points in each wave -1, and *betai* is the incomplete beta function. To get the critical value for the upper one-tail test we solve F(x)=1-alpha. For the lower one-tail test we solve F(x)=alpha. In the two-tailed test the lower critical value is a solution for F(x)=alpha/2 and the upper critical value is a solution for F(x)=1-alpha/2.

### *See Also* {#see-also}
[Statistical Analysis](/igorpro/analysis/statistics.md), [StatsVariancesTest](/igorpro/commands/statsvariancestest.md), [StatsFCDF](/igorpro/commands/statsfcdf.md), [betai](/igorpro/commands/betai.md)

### *Demos* {#demos}
[Open F-Test Demo.pxp](#igor-pxp/Examples/Statistics/F-Test__Demo.pxp)