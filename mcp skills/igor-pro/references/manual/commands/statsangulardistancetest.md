---
description: "The StatsAngularDistanceTest operation performs nonparametric tests on the angular distance between sample data and reference directions for two or more…"
slug: /commands/statsangulardistancetest
---

<div className="command-signature">

## <strong>StatsAngularDistanceTest</strong>  [/ALPH=<em>significance</em> /APRX=<em>m</em> /T=<em>k</em> /Q/Z /WSTR=<em>waveListString</em> ] [<em>srcWave1</em>, <em>srcWave2</em>, <em>srcWave3</em>... ] {#statsangulardistancetest}

</div>

The StatsAngularDistanceTest operation performs nonparametric tests on the angular distance between sample data and reference directions for two or more samples in individual waves. The angular distance is the shortest distance between two points on a circle (in radians). Specify the sample waves using /WSTR or by listing them following the flags. Set reference directions with /ANG, /ANGW, or the sample mean direction.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/ALPH = *val*</span> | Sets the significance level (default 0.05). |
| <span class="table-cell-nowrap">/ANG = {*d1*, *d2* }</span> | Sets reference directions (in radians) for two samples; for more than two samples use /ANGW. |
| <span class="table-cell-nowrap">/ANGM</span> | Computes the mean direction of each sample and uses it as the reference direction. |
| <span class="table-cell-nowrap">/ANGW = *dWave*</span> | Sets reference directions (in radians) for more than two samples using directions in *dWave*, which must be single or double precision. |
| <span class="table-cell-nowrap">/APRX = *m*</span> | Controls the approximation method for computing the P-value in the case of two samples (Mann-Whitney Wilcoxon). See [StatsWilcoxonRankTest](/igorpro/commands/statswilcoxonranktest.md) for more details. The default value is 0, which may require long computation times if your sample size is large. Use /APRX=1 if you have a large sample and you expect ties in the data. |
| <span class="table-cell-nowrap">/Q</span> | No results printed in the history area. |
| <span class="table-cell-nowrap">/T = *k*</span> | Displays results in a table. *k*  specifies the table behavior when it is closed. |
|  |<table class="nested-table"><tbody><tr><td>*k*&nbsp;=0:</td><td>Normal with dialog (default).</td></tr><tr><td>*k*&nbsp;=1:</td><td>Kills with no dialog.</td></tr><tr><td>*k*&nbsp;=2:</td><td>Disables killing.</td></tr></tbody></table>
| <span class="table-cell-nowrap">/TAIL = *tail*</span> | *tail*  is a bitwise parameter that controls tail handling. |
|  |<table class="nested-table"><tbody><tr><td>Bit&nbsp;0:</td><td>Lower tail.</td></tr><tr><td>Bit&nbsp;1:</td><td>Upper tail (default).</td></tr><tr><td>Bit&nbsp;2:</td><td>Two tail.</td></tr></tbody></table>
|  | See [Setting Bit Parameters](/igorpro/programming/commands.md#setting-bit-parameters) for details about bit settings. |
|  | The P-Value corresponding to the last tail calculated will be entered in the table. |
| <span class="table-cell-nowrap">/WSTR = *waveListString*</span> |  |
|  | Specifies a string containing a semicolon-separated list of waves that contain sample data. Use *waveListString*  instead of listing each wave after the flags. |
| <span class="table-cell-nowrap">/Z</span> | Ignores errors. V_flag will be set to -1 for any error and to zero otherwise. |

### *Details* {#details}
The inputs for StatsAngularDistanceTest are two or more waves each corresponding to individual sample. The waves must be single or double precision expressing the angles in radians. There is no restriction on the number of points or dimensionality of the waves but the data should not contain NaNs or INFs. We recommend that you use double precision waves, especially if there are ties in the data. The reference directions should also be in radians. For two samples, StatsAngularDistanceTest computes the angular distances between the input data and the reference directions and then uses the Mann-Whitney-Wilcoxon test ([StatsWilcoxonRankTest](/igorpro/commands/statswilcoxonranktest.md)). Results are stored in the W_WilcoxonTest wave and in the corresponding table. For more than two samples, StatsAngularDistanceTest uses the Kruskal-Wallis test, storing results in the wave W_KWTestResults wave in the current data folder.

V_flag will be set to -1 for any error and to zero otherwise.

### *References* {#references}
See, in particular, Chapter 27 of:

Zar, J.H., *Biostatistical Analysis*, 4th ed., 929 pp., Prentice Hall, Englewood Cliffs, New Jersey, 1999.

### *See Also* {#see-also}
[Statistical Analysis](/igorpro/analysis/statistics.md), [StatsWilcoxonRankTest](/igorpro/commands/statswilcoxonranktest.md), [StatsKWTest](/igorpro/commands/statskwtest.md)

### *Demos* {#demos}
[Open Angular Distance Demo](#igor-pxp/Examples/Statistics/Circular__Statistics/Angular__Distance__Test.pxp)