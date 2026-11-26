---
description: "The StatsNPNominalSRTest operation performs a nonparametric serial randomness test for nominal data consisting of two types."
slug: /commands/statsnpnominalsrtest
---

<div className="command-signature">

## <strong>StatsNPNominalSRTest</strong>  [/ALPH=<em>alpha</em>  /P={<em>m</em>,<em>n</em>,<em>u</em> }/T=<em>k</em> /Z/Q] [<em>srcWave</em> ] {#statsnpnominalsrtest}

</div>

The StatsNPNominalSRTest operation performs a nonparametric serial randomness test for nominal data consisting of two types. The null hypothesis is that the data are randomly distributed. Output is to the W_StatsNPSRTest wave in the current data folder.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/ALPH = *val*</span> | Sets the significance level (default *val* =0.05). |
| <span class="table-cell-nowrap">/DEST = *dstWave*</span> | Specify the destination wave for the nonparametric serial randomness test results.  If you do not use this flag, the results are stored in the wave W_StatsNPSRTest in the current data folder. |
|  | This flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/FREE</span> | Creates the user-specified destination wave as a free wave. |
|  | /FREE is allowed only in functions, and only if the destination waves are simple names or wave reference structure fields. |
|  | See [Free Waves](/igorpro/programming/programming.md#free-waves) for more discussion. |
|  | The /FREE flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/P = {*m*,*n*,*u* }</span> | Provides a summary of the data instead of providing the nominal series. *m* is the number of elements of the first type, *n* is the number of elements of the second type, and *u* is the number of runs or contiguous sequences of each type. Do not use *srcWave* with /P. |
| <span class="table-cell-nowrap">/Q</span> | No results printed in the history area. |
| <span class="table-cell-nowrap">/T = *k*</span> | Displays results in a table. *k* specifies the table behavior when it is closed. |
|  |<table class="nested-table"><tbody><tr><td>*k*&nbsp;=0:</td><td>Normal with dialog (default).</td></tr><tr><td>*k*&nbsp;=1:</td><td>Kills with no dialog.</td></tr><tr><td>*k*&nbsp;=2:</td><td>Disables killing.</td></tr></tbody></table>
| <span class="table-cell-nowrap">/Z</span> | Ignores errors. |

### *Details* {#details}
The input wave to StatsNPNominalSRTest is specified with *srcWave* or /P. The wave must contain exactly two values. If *srcWave* is a text wave, then each type can be designated by a letter or by a short string (less than 200 bytes). If *srcWave* is numeric, you should avoid the usual floating point waves, which can give rise to internal representations of more than two distinct values. Output to W_StatsNPSRTest includes the total number of points (*N*), the number of occurrences (*m*) of the first variable, the number of occurrences (*n*) of the second variable, and the number of runs (*u*). When both *m* and *n* are less than 300, it computes the P value [probability P(*u*'<*u*)]  and the critical values using the Swed and Eisenhart algorithm. When *m* or *n* are larger than 300, it computes the mean and standard deviation of an equivalent normal distribution with the corresponding critical value.

### *References* {#references}
Swed, F.S., and C. Eisenhart, Tables for testing randomness of grouping in a sequence of alternatives, *Ann. Math. Statist.*, *14*, 66-87, 1943..

See, in particular, Chapter 25 of:

Zar, J.H., *Biostatistical Analysis*, 4th ed., 929 pp., Prentice Hall, Englewood Cliffs, New Jersey, 1999.

### *See Also* {#see-also}
[Statistical Analysis](/igorpro/analysis/statistics.md), [StatsSRTest](/igorpro/commands/statssrtest.md)

### *Demos* {#demos}
[Open NominalSR Demo.pxp](#igor-pxp/Examples/Statistics/NominalSR__Demo.pxp)