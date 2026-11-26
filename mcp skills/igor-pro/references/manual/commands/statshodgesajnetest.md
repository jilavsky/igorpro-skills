---
description: "The StatsHodgesAjneTest operation performs the Hodges-Ajne nonparametric test for uniform distribution around a circle."
slug: /commands/statshodgesajnetest
---

<div className="command-signature">

## <strong>StatsHodgesAjneTest</strong>  [/ALPH=<em>significance</em> /Q/SA=<em>specAngle</em> /Z /T=<em>k</em> ] <em>srcWave</em> {#statshodgesajnetest}

</div>

The StatsHodgesAjneTest operation performs the Hodges-Ajne nonparametric test for uniform distribution around a circle. Output is to the W_HodgesAjne wave in the current data folder or optionally to a table.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/ALPH = *val*</span> | Sets the significance level (default *val* =0.05). |
| <span class="table-cell-nowrap">/Q</span> | No results printed in the history area. |
| <span class="table-cell-nowrap">/SA = *specAngle*</span> | Uses the Batschelet modification of the Hodges-Ajne test to test for uniformity against the alternative of concentration around the specified angle. *specAngle* must be expressed in radians modulus 2π. |
| <span class="table-cell-nowrap">/T = *k*</span> | Displays results in a table. *k* specifies the table behavior when it is closed. |
|  |<table class="nested-table"><tbody><tr><td>*k*&nbsp;=0:</td><td>Normal with dialog (default).</td></tr><tr><td>*k*&nbsp;=1:</td><td>Kills with no dialog.</td></tr><tr><td>*k*&nbsp;=2:</td><td>Disables killing.</td></tr></tbody></table>
| <span class="table-cell-nowrap">/Z</span> | Ignores errors. V_flag will be set to -1 for any error and to zero otherwise. |

### *Details* {#details}
The input *srcWave* must contain angles in radians, can be any number of dimensions, can be single or double precision, and should not contain NaNs or INFs.

StatsHodgesAjneTest performs the standard Hodges-Ajne test, which simply tests for uniformity against the hypothesis that the population is not uniformly distributed around the circle. This test finds a diameter that divides the circle into two halves such that one contains the least number of data *m*, the test statistic.

Use /SA to perform the modified (Batschelet) test, which tests against the alternative that the population is concentrated somehow about the specified angle. The modified test counts the number of points m' in 90-degree neighborhoods around the specified angle. The test statistic is given by C=*n*-*m*' where *n* is the number of points in the wave. The critical value is computed from the binomial probability density.

In both cases H0 is rejected if the statistic is smaller than the critical value.

### *References* {#references}
Ajne, B., A simple test for uniformity of a circular distribution, *Biometrica*, *55*, 343-354, 1968.

See, in particular, Chapter 27 of:

Zar, J.H., *Biostatistical Analysis*, 4th ed., 929 pp., Prentice Hall, Englewood Cliffs, New Jersey, 1999.

### *See Also* {#see-also}
[Statistical Analysis](/igorpro/analysis/statistics.md), [StatsCircularMeans](/igorpro/commands/statscircularmeans.md), [StatsCircularMoments](/igorpro/commands/statscircularmoments.md), [StatsWatsonUSquaredTest](/igorpro/commands/statswatsonusquaredtest.md), [StatsWatsonWilliamsTest](/igorpro/commands/statswatsonwilliamstest.md), [StatsWheelerWatsonTest](/igorpro/commands/statswheelerwatsontest.md)

### *Demos* {#demos}
[Open Hodges-Ajne Demo.pxp](#igor-pxp/Examples/Statistics/Circular__Statistics/Hodges-Ajne__Demo.pxp)