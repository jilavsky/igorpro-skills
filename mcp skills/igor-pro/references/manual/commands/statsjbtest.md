---
description: "The StatsJBTest operation performs the Jarque-Bera test on srcWave. Output is to the W_JBResults wave in the current data folder."
slug: /commands/statsjbtest
---

<div className="command-signature">

## <strong>StatsJBTest</strong>  [/ALPH=<em>alpha</em>  /T=<em>k</em> /Z/Q] <em>srcWave</em> {#statsjbtest}

</div>

The StatsJBTest operation performs the Jarque-Bera test on *srcWave*. Output is to the W_JBResults wave in the current data folder.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/ALPH = *val*</span> | Sets the significance level (default *val* =0.05). |
| <span class="table-cell-nowrap">/DEST = *wrWave*</span> | Specify the destination wave for the Jarque-Bera test results.  If you do not use this flag, the operation saves the output in the wave W_JBResults in the current data folder. |
|  | This flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/FREE</span> | Creates the user-specified destination wave as a free wave. |
|  | /FREE is allowed only in functions, and only if the destination waves are simple names or wave reference structure fields. |
|  | See [Free Waves](/igorpro/programming/programming.md#free-waves) for more discussion. |
|  | The /FREE flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/Q</span> | No results printed in the history area. |
| <span class="table-cell-nowrap">/T = *k*</span> | Displays results in a table. *k* specifies the table behavior when it is closed. |
|  |<table class="nested-table"><tbody><tr><td>*k*&nbsp;=0:</td><td>Normal with dialog (default).</td></tr><tr><td>*k*&nbsp;=1:</td><td>Kills with no dialog.</td></tr><tr><td>*k*&nbsp;=2:</td><td>Disables killing.</td></tr></tbody></table>
| <span class="table-cell-nowrap">/Z</span> | Ignores errors. V_flag will be set to -1 for any error and to zero otherwise. |

### *Details* {#details}
StatsJBTest computes the Jarque-Bera statistic

$$
\displaystyle J B=\frac{n}{6}\left(S^{2}+\frac{K^{2}}{4}\right),
$$

where *S* is the skewness, *K* is the kurtosis, and *n* is the number of points in the input wave. We can express *S* and *K* terms of the *j*th moment of the distribution for n samples *X*<sub>i</sub>

$$
\displaystyle \mu_{j}=\frac{1}{n} \sum_{i=1}^{n}\left(X_{i}-\bar{X}\right)^{j}
$$

as

$$
\displaystyle S=\frac{\mu_{3}}{\left(\mu_{2}\right)^{3 / 2}},
$$

and

$$
\displaystyle K=\frac{\mu_{4}}{\left(\mu_{2}\right)^{2}}-3 .
$$

The Jarque-Bera statistic is asymptotically distributed as a Chi-squared with two degrees of freedom. For values of *n* in the range [7,2000] the operation provides critical values obtained from Monte-Carlo simulations. For further details or if you would like to run your own simulation to obtain critical values for other values of *n*, use the JarqueBeraSimulation example experiment.

StatsJBTest reports the number of finite data points, skewness, kurtosis, Jarque-Bera statistic, asymptotic critical value, and the critical value obtained from Monte-Carlo calculations as appropriate; it ignores NaNs and INFs.

### *References* {#references}
Jarque, C., and A. Bera, A test of normality of observations and regression residuals, *International Statistical Review*, *55*, 163-172, 1987.

### *See Also* {#see-also}
[Statistical Analysis](/igorpro/analysis/statistics.md), [StatsKSTest](/igorpro/commands/statskstest.md), [WaveStats](/igorpro/commands/wavestats.md), [StatsCircularMoments](/igorpro/commands/statscircularmoments.md)

### *Demos* {#demos}
[Open Jarque-Bera Simulation.pxp](#igor-pxp/Examples/Statistics/Jarque-Bera__Simulation.pxp)