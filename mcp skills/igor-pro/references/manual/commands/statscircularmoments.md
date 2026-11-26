---
description: "The StatsCircularMoments operation computes circular statistical moments and optionally performs angular uniformity tests for the data in srcWave."
slug: /commands/statscircularmoments
---

<div className="command-signature">

## <strong>StatsCircularMoments</strong>  [/ALPH=<em>alpha</em> /AXD=<em>p</em> /CYCL=<em>cycle</em> /GRPD={<em>start</em>, <em>delta</em> } /KUPR/LOS/M=<em>moment</em> /MODE=<em>mode</em> /ORGN=<em>origin</em> /Q/RAYL[=<em>meanDirection</em> ]/SAW/T=<em>k</em> /Z] <em>srcWave</em> {#statscircularmoments}

</div>

The StatsCircularMoments operation computes circular statistical moments and optionally performs angular uniformity tests for the data in *srcWave*. The extent of the calculation is determined by the requested moment. The default results are stored in the W_CircularStats wave in the current data folder and are optionally displayed in a table. Additional results are listed under the corresponding flags.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/ALPH = *alpha*</span> | Sets an *alpha* value for computing confidence intervals (default is 0.05). |
| <span class="table-cell-nowrap">/AXD = *p*</span> | Designates the input as p-axial data. For example, if the input represents undirected lines then *p* =2 and the operation multiplies the angles by a factor *p* (after shifting /ORGN and accounting for /CYCL). It does not back-transform the mean or median axis. |
| <span class="table-cell-nowrap">/CYCL = *cycle*</span> | Specifies the length of the data cycle. You do not need to do so if you are using one of the built-in modes, but this is still a useful option, as for setting the length of a particular month when using /MODE=5. |
| <span class="table-cell-nowrap">/DSTA = *aWave*</span> | Specify the destination wave for the translated angle (/SAW).  If you do not use this flag, the operation saves this output in the wave W_AngleWave in the current data folder. |
|  | This flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/DSTC = *sWave*</span> | Specify the destination wave for the circular moments test results.  If you do not use this flag, the operation saves this output in the wave W_CircularStats in the current data folder. |
|  | This flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/DSTL = *loWave*</span> | Specify the destination wave for the linear order statistics (/LOS).  If you do not use this flag, the operation saves this output in the wave W_LinearOrderStats in the current data folder. |
|  | This flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/FREE</span> | Creates all user-specified destination waves as free waves. |
|  | /FREE is allowed only in functions, and only if the destination waves are simple names or wave reference structure fields. |
|  | See [Free Waves](/igorpro/programming/programming.md#free-waves) for more discussion. |
|  | The /FREE flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/GRPD = {*start*, *delta* }</span> |  |
|  | Computes circular statistics for grouped data. In this case *srcWave* contains frequencies or the number of events that belong to a particular angle group. There are as many groups as there are elements in *srcWave*. The first group is centered at start radians and each consecutive group is centered delta radians away. You must set both the start and delta to sensible values. *srcWave* may contain NaNs but it is an error if all values are NaN. The only other flags that work in combination with this flag are /Q, /T, and /Z. |
| <span class="table-cell-nowrap">/KUPR[* = k*]</span> | Tests the uniformity of a circular distribution of ungrouped data using the Kuiper statistic. The data are converted into a set {x<sub>i</sub>} by normalizing the input angles to the range [0,1], ranking the results then using the two quantities D<sub>+</sub> and D<sub>-</sub> to compute the Kuiper statistic. Use *k*=0 for Fisher's version: |
|  | $$ \displaystyle \mathrm{V}=\left(D_{+}+D_{-}\right)(\sqrt{\mathrm{n}}+0.155+0.24 / \sqrt{\mathrm{n}}) . $$ |
|  | Use k=1, added in Igor Pro 8.00, for the more common definition of the Kuiper statistic: |
|  | $$ \displaystyle V=\left(D_{+}+D_{-}\right) . $$ |
|  | Here |
|  | $$ \displaystyle D_{+}=\operatorname{Max} \text { of: } \frac{1}{\mathrm{n}}-\mathrm{x}_{0}, \frac{2}{\mathrm{n}}-\mathrm{x}_{1}, \ldots, 1-\mathrm{x}_{\mathrm{n}-1}, $$ |
|  | $$ \displaystyle D_{-}=\operatorname{Max} \text { of: } \mathrm{x}_{0}, \mathrm{x}_{1-\frac{1}{n}}, \ldots, \mathrm{x}_{\mathrm{n}-1-\frac{\mathrm{n}-1}{\mathrm{n}}}, $$ |
|  | and *n* is the number of valid points in *srcWave*. You can find the results in the wave W_CircularStats under row label "Kuiper V" and "Kuiper CDF(V)". See Fisher and Press *et al*. for more information. |
| <span class="table-cell-nowrap">/LOS</span> | Computes Linear Order Statistics by sorting the angle values from small to large, dividing each angle by 2π and shifting the origin so that the output range is [0,1]. The results are stored in the wave W_LinearOrderStats in the current data folder. The X scaling of the wave is set so that the offset and the delta are 1/(n+1) where n is the number of non-NaN points in the input. |
| <span class="table-cell-nowrap">/M = *moment*</span> | Computes specified moments. By default, it computes the second order moments as well as skewness, kurtosis, median, and mean deviation. Use /M=1 for the first moment. For higher moments, both the specified moment and all the default quantities are computed. |
| <span class="table-cell-nowrap">/MODE = *mode*</span> | Handles special types of data. |
|  |<table class="nested-table"><tbody><tr><td>***mode***</td><td>**Data in *srcWave***</td></tr><tr><td>0</td><td>Angles in radians [0,2π] (default).</td></tr><tr><td>1</td><td>Angles in radians [-π, π].</td></tr><tr><td>2</td><td>Angles in degrees [0,360].</td></tr><tr><td>3</td><td>Angles in degrees [-180,180].</td></tr><tr><td>4</td><td>Igor date format for 1 year cycles.</td></tr><tr><td>5</td><td>Igor date format for one month cycle.</td></tr><tr><td>6</td><td>Igor date format for one week cycle.</td></tr><tr><td>7</td><td>Igor date format for one day cycle.</td></tr><tr><td>8</td><td>Igor date format for one hour cycle.</td></tr></tbody></table>
| <span class="table-cell-nowrap">/ORGN = *origin*</span> | Specifies the origin of the data (the value corresponding to an angle of zero degrees). For example, if you are using Igor date format and you want the origin to be the first second in year YYYY, use /ORGN=(date2secs(YYYY,1,1)). |
| <span class="table-cell-nowrap">/Q</span> | No results printed in the history area. |
| <span class="table-cell-nowrap">/RAYL[ = *meanDirection* ]</span> |  |
|  | Performs the Rayleigh test for uniformity. If the "alternative" mean direction is specified (in radians), the test computes |
|  | r0Bar=rBar cos(tBar-*meanDirection* ) |
|  | and then computes the significance probability of r0Bar. The null hypothesis H<sub>0</sub> corresponds to uniformity. It is rejected when r0Bar is too large. If the mean direction is not specified then r0Bar is rBar which is always calculated as part of the first moments so the operation only computes the relevant significance probability (P-Value). The critical values for both cases are computed according to Durand and Greenwood. |
| <span class="table-cell-nowrap">/SAW</span> | Saves the translated angle data in the wave W_AngleWave in the current data folder.  The translated angle is the processed raw angle from *srcWave* adjusted for the origin specified by the /ORGN flag and the cycles specified by /MODE. |
| <span class="table-cell-nowrap">/T = *k*</span> | Displays results in a table. *k* specifies the table behavior when it is closed. |
|  |<table class="nested-table"><tbody><tr><td>*k*&nbsp;=0:</td><td>Normal with dialog (default).</td></tr><tr><td>*k*&nbsp;=1:</td><td>Kills with no dialog.</td></tr><tr><td>*k*&nbsp;=2:</td><td>Disables killing.</td></tr></tbody></table>
|  | The table is associated with the test and not with the data. If you repeat the test, it will update the table with the new results unless you moved the output wave to a different data folder. If the named table exists but it does not display the output wave from the current data folder, the table is renamed and a new table is created.. |
| <span class="table-cell-nowrap">/Z</span> | Ignores errors. V_flag will be set to -1 for any error and to zero otherwise. |

### *Details* {#details}
StatsCircularMoments is equivalent to [WaveStats](/igorpro/commands/wavestats.md) but it applies to circular data, which are distributed on the perimeter of a circle representing some period or cycle. If your data are not described by one of the built-in modes, you can specify the value of the origin (/ORGN), which is mapped to zero degrees and the size of a cycle or period.

When you use Igor date formats with the built-in modes for dates, the default origin is set to zero. The default cycle in the case of Mode 4 is 366. This is done in order to handle both leap and nonleap years. Similarly, Mode 5 uses a cycle of 31 days. Note that the internal conversion from Igor date to (year, month, day) is independent of the cycle specification and is therefore not affected by this choice. You should use the /CYCL flag if you use one of these modes with a fixed size of year or month.

The parameters listed below are computed and displayed (see row labels) in the table.  Here *N* is the number of valid (non-NaN) angles {θ<sub>i</sub>}

$$
\displaystyle \mathrm{C}=\sum_{i=1}^{n} \cos \theta_{i}
$$

$$
\displaystyle \mathrm{S}=\sum_{i=1}^{n} \sin \theta_{i}
$$

$$
\displaystyle R=\sqrt{C^{2}+S^{2}}
$$

$$
\displaystyle c B a r=\bar{C}=C / n
$$

$$
\displaystyle s B a r=\bar{S}=S / n
$$

$$
\displaystyle r B a r=\bar{R}=R / n
$$

$$
\displaystyle \text { tBar }=\bar{\theta}=\left\{\begin{array}{ll}
\operatorname{atan}(S / C) & S>0, C>0 \\
\\
\operatorname{atan}(S / C)+\pi & C<0 \\
\\
\operatorname{atan}(S / C)+2 \pi & S<0, C>0
\end{array}\right.
$$

$$
\displaystyle V=1-\bar{R}
$$

$$
\displaystyle v=\sqrt{-2 \ln (1-V)}
$$

median is the value which minimizes

$$
\displaystyle d(\theta)=\pi-\frac{1}{n} \sum_{i=1}^{n}\left|\pi-\left|\theta_{i}-\bar{\theta}\right|\right|
$$

mean deviation = The minimum of the last equation when θ -> median.

Higher order moments are denoted with the moment number such that t3Bar is the uncentered third moment of the angle while primed quantities are relative to mean direction tBar.  Using this notation

$$
\displaystyle \widehat{\rho_{2}}=\frac{1}{n} \sum_{i=1}^{n} \cos 2\left(\theta_{i}-\bar{\theta}\right)
$$

$$
\displaystyle \text { circular dispersion }=\frac{1-\widehat{\rho_{2}}}{2 \bar{R}^{2}}
$$

$$
\displaystyle \text { skewness }=\frac{\widehat{\rho}_{2} \sin \left(\hat{\mu}_{2}^{\prime}-2 \bar{\theta}\right)}{(1-\bar{R})^{3 / 2}}
$$

$$
\displaystyle \text { kurtosis }=\frac{\widehat{\rho_{2}} \cos \left(\hat{\mu}_{2}^{\prime}-2 \bar{\theta}\right)-\bar{R}^{4}}{(1-\bar{R})^{2}}
$$

where

$$
\displaystyle \hat{\mu}_{p}^{\prime}=\left\{\begin{array}{ll}
\operatorname{atan}\left(S_{p} / C_{p}\right) & S_{p}>0, C_{p}>0 \\
\\
\operatorname{atan}\left(S_{p} / C_{p}\right)+\pi & C_{p}<0 \\
\\
\operatorname{atan}\left(S_{p} / C_{p}\right)+2 \pi & S_{p}<0, C_{p}>0
\end{array}\right.
$$

and

$$
\displaystyle C_{p}=\frac{1}{n} \sum_{i=1}^{n} \cos p \theta_{i}, \quad S_{p}=\frac{1}{n} \sum_{i=1}^{n} \sin p \theta_{i} .
$$

### *References* {#references}
Fisher, N.I., *Statistical Analysis of Circular Data*, 295pp., Cambridge University Press, New York, 1995.

Press, William H., et al., *Numerical Recipes in C*, 2nd ed., 994 pp., Cambridge University Press, New York, 1992.

Durand, D., and J.A. Greenwood, Modifications of the Rayleigh test for uniformity in analysis of two-dimensional orientation data, *J. Geol., 66*, 229-238, 1958..

### *See Also* {#see-also}
[Statistical Analysis](/igorpro/analysis/statistics.md), [WaveStats](/igorpro/commands/wavestats.md), [StatsAngularDistanceTest](/igorpro/commands/statsangulardistancetest.md), [StatsCircularCorrelationTest](/igorpro/commands/statscircularcorrelationtest.md), [StatsCircularMeans](/igorpro/commands/statscircularmeans.md), [StatsHodgesAjneTest](/igorpro/commands/statshodgesajnetest.md), [StatsWatsonUSquaredTest](/igorpro/commands/statswatsonusquaredtest.md), [StatsWatsonWilliamsTest](/igorpro/commands/statswatsonwilliamstest.md), [StatsWheelerWatsonTest](/igorpro/commands/statswheelerwatsontest.md)

### *Demos* {#demos}
[Open Circular Moments Demo.pxp](#igor-pxp/Examples/Statistics/Circular__Statistics/Circular__Moments__Demo.pxp)