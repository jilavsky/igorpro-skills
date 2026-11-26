---
description: "The StatsCircularTwoSampleTest operation performs second order analysis of angles."
slug: /commands/statscirculartwosampletest
---

<div className="command-signature">

## <strong>StatsCircularTwoSampleTest</strong>  [/ALPH=<em>alpha</em>  /T=<em>k</em>  /NSOA /NPR /PSOA /PPR /Z /Q ] <em>waveA</em>, <em>waveB</em> {#statscirculartwosampletest}

</div>

The StatsCircularTwoSampleTest operation performs second order analysis of angles. Using the appropriate flags you can choose between parametric or nonparametric, unordered or paired tests. The input consists of two waves that contain one or two columns. The first column contains angle data (mean angles) expressed in radians and an optional second column that contains associated vector lengths. The waves are expected to be either single or double precision. Results are stored in the W_StatsCircularTwoSamples wave in the current data folder and optionally displayed in a table. Some of the tests may have additional outputs.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/ALPH = *val*</span> | Sets the significance level (default *val* =0.05). |
| <span class="table-cell-nowrap">/DSTC = *sWave*</span> | Specify the destination wave for the circular two sample test results.  If you do not use this flag the operation saves this output in the wave W_StatsCircularTwoSamples in the current data folder. |
|  | This flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/DSTW = *wWave*</span> | Specify the destination wave for the nonparametric second order two-sample test results (/NSOA).  If you do not use this flag, the operation saves this output in the wave W_WatsonUtest in the current data folder. |
|  | This flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/FREE</span> | Creates all the user-specified destination waves as free waves. |
|  | /FREE is allowed only in functions, and only if the destination waves are simple names or wave reference structure fields. |
|  | See [Free Waves](/igorpro/programming/programming.md#free-waves) for more discussion. |
|  | The /FREE flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/NPR</span> | Performs nonparametric paired-sample test (Moore). The input waves must contain paired angular data so both must have single column and the same number of points. |
| <span class="table-cell-nowrap">/NSOA</span> | Perform nonparametric second order two-sample test. Input waves must each contain two columns. |
| <span class="table-cell-nowrap">/PPR</span> | Performs parametric paired-sample test. Input waves must contain paired data and must have the same number of points. |
| <span class="table-cell-nowrap">/PSOA</span> | Performs parametric second order analysis of two samples. The input waves must each contain two columns. |
| <span class="table-cell-nowrap">/Q</span> | No information printed in the history area. |
| <span class="table-cell-nowrap">/T = *k*</span> | Displays results in a table. *k* specifies the table behavior when it is closed. |
|  |<table class="nested-table"><tbody><tr><td>*k*&nbsp;=0:</td><td>Normal with dialog (default).</td></tr><tr><td>*k*&nbsp;=1:</td><td>Kills with no dialog.</td></tr><tr><td>*k*&nbsp;=2:</td><td>Disables killing.</td></tr></tbody></table>
| <span class="table-cell-nowrap">/Z</span> | Ignore any errors.  The variable V_Flag is set to 0 if there are no errors, or to -1 otherwise. |

### *Details* {#details}
The nonparametric paired-sample test (/NPR) is Moore's test for paired angles applied in second order analysis. The input can consist of one or two column waves. When both waves contain a single column the operation proceeds as if all the vector length were identically 1. The Moore statistic (H<sub>0</sub> -> pair equality) is computed and compared to the critical value from the Moore distribution (see [StatsInvMooreCDF](/igorpro/commands/statsinvmoorecdf.md)).

The nonparametric second-order two-sample test (/NSOA) consists of pre-processing where the grand mean is subtracted from the two inputs followed by application of Watson's U<sup>2</sup> test ([StatsWatsonUSquaredTest](/igorpro/commands/statswatsonusquaredtest.md)) with H<sub>0</sub> implying that the two samples came from the same population. The results of this test are stored in the wave W_WatsonUtest.

The parametric paired-sample test (/PPR) is due to Hotelling. In this test the input should consist of both angular and vector length data. The test statistic is compared with a critical value from the F distribution ([StatsInvFCDF](/igorpro/commands/statsinvfcdf.md)).

The parametric second order two-sample test (/PSOA) is an extension of Hotelling one-sample test to second order analysis where an F-like statistic is computed corresponding to H<sub>0</sub> of equal mean angles.

### *References* {#references}
Zar, J.H., *Biostatistical Analysis*, 4th ed., 929 pp., Prentice Hall, Englewood Cliffs, New Jersey, 1999.

### *See Also* {#see-also}
[Statistical Analysis](/igorpro/analysis/statistics.md), [StatsInvMooreCDF](/igorpro/commands/statsinvmoorecdf.md), [StatsWatsonUSquaredTest](/igorpro/commands/statswatsonusquaredtest.md), [StatsInvFCDF](/igorpro/commands/statsinvfcdf.md)