---
description: "The StatsANOVA1Test operation performs a one-way ANOVA test (fixed-effect model)."
slug: /commands/statsanova1test
---

<div className="command-signature">

## <strong>StatsANOVA1Test</strong>  [/ALPH=<em>significance</em> /BF/Q/Z/T=<em>k</em> /W/WSTR=<em>wList</em>]  [<em>wave1</em>,<em>wave2</em>,... <em>wave100</em> ] {#statsanova1test}

</div>

The StatsANOVA1Test operation performs a one-way ANOVA test (fixed-effect model). The standard ANOVA test results are stored in the M_ANOVA1 wave in the current data folder.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/ALPH = *val*</span> | Sets the significance level (default 0.05). |
| <span class="table-cell-nowrap">/BF</span> | Performs the Brown and Forsythe test computing F'' and degrees of freedom. The W_ANOVA1BnF wave in the current data folder contains the output. |
| <span class="table-cell-nowrap">/DSTA = *aWave*</span> | Specify the output wave for the standard ANOVA test results.  If you do not specify this flag, the operation stores the data in the wave M_ANOVA1 in the current data folder. |
|  | This flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/DSTB = *bWave*</span> | Specify the output wave for the Brown and Forsythe test results.  If you do not specify this flag, the operation stores the data in the wave W_ANOVA1BnF in the current data folder. |
|  | This flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/DSTW = *wWave*</span> | Specify the output wave for the Welch test.  If you do not specify this flag, the operation stores the data in the wave W_ANOVA1Welch in the current data folder. |
|  | This flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/FREE</span> | Creates all destination waves as free waves.  This flag does not affect any of the output waves that are created by default without a user-specified destination. |
|  | /FREE is allowed only in functions, and only if the destination waves are simple names or wave reference structure fields. |
|  | See [Free Waves](/igorpro/programming/programming.md#free-waves) for more discussion. |
|  | The /FREE flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/Q</span> | No results printed in the history area. |
| <span class="table-cell-nowrap">/T = *k*</span> | Displays results in a table; additional tables are created with /BF and /W. |
|  | *k*  specifies the table behavior when it is closed. |
|  |<table class="nested-table"><tbody><tr><td>*k*&nbsp;=0:</td><td>Normal with dialog (default).</td></tr><tr><td>*k*&nbsp;=1:</td><td>Kills with no dialog.</td></tr><tr><td>*k*&nbsp;=2:</td><td>Disables killing.</td></tr></tbody></table>
| <span class="table-cell-nowrap">/W</span> | Performs the Welch test F' and computes degrees of freedom. The W_ANOVA1Welch wave in the current data folder contains the output. |
| <span class="table-cell-nowrap">/WSTR = *waveListString*</span> |  |
|  | Specifies a string containing a semicolon-separated list of waves that contain sample data. Use *waveListString*  instead of listing each wave after the flags. |
| <span class="table-cell-nowrap">/Z</span> | Ignores errors. V_flag will be set to -1 for any error and to zero otherwise. |

### *Details* {#details}
Inputs to StatsANOVA1Test are two or more 1D numerical waves containing (one wave for each group of samples). Use NaN for missing entries or use waves with different numbers of points. The standard ANOVA results are in the M_ANOVA1 wave with corresponding row and column labels. Use /T to display the results in a table. In each case you will get the two degrees of freedom values, the F value, the critical value Fc for the choice of alpha and the degrees of freedom, and the P-value for the result. V_flag will be set to -1 for any error and to zero otherwise.

In some cases the ANOVA test may not be appropriate. For example, if groups do not exhibit sufficient homogeneity of variances. Although this may not be fatal for the ANOVA test, you may get more insight by performing the variances test in [StatsVariancesTest](/igorpro/commands/statsvariancestest.md).

If there are only two groups this test should be equivalent to [StatsTTest](/igorpro/commands/statsttest.md).

You can evaluate the power of an ANOVA test for a given set of degrees of freedom and noncentrality parameter using:


```igor
power=1-StatsNCFCDF(StatsInvFCDF((1-alpha),n1,n2),n1,n2,delta)
```

Here n1 is the Groups' degrees of freedom, n2 is the Error degrees of freedom and delta is the noncentrality parameter.  For more information see ANOVA Power Calculations Panel and the associated example experiment.

### *References* {#references}
Zar, J.H., *Biostatistical Analysis*, 4th ed., 929 pp., Prentice Hall, Englewood Cliffs, New Jersey, 1999.

### *See Also* {#see-also}
[Statistical Analysis](/igorpro/analysis/statistics.md), [StatsVariancesTest](/igorpro/commands/statsvariancestest.md), [StatsTTest](/igorpro/commands/statsttest.md), [StatsNCFCDF](/igorpro/commands/statsncfcdf.md), [StatsInvFCDF](/igorpro/commands/statsinvfcdf.md)

### *Demos* {#demos}
[Open ANOVA1 Demo.pxp](#igor-pxp/Examples/Statistics/ANOVA1__Demo.pxp)