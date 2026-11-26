---
description: "The StatsKSTest operation performs the Kolmogorov-Smirnov (KS) goodness-of-fit test for two continuous distributions."
slug: /commands/statskstest
---

<div className="command-signature">

## <strong>StatsKSTest</strong>  [/ALPH=<em>alpha</em>  /CDFF=<em>func</em>  /T=<em>k</em> /Z/Q] <em>srcWave</em>  [, <em>distWave</em> ] {#statskstest}

</div>

The StatsKSTest operation performs the Kolmogorov-Smirnov (KS) goodness-of-fit test for two continuous distributions. The first distribution is *srcWave* and the second distribution can be expressed either as the optional wave *distWave* or as a user function with /CDFF. Output is to the W_KSResults wave in the current data folder.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/ALPH = *val*</span> | Sets the significance level (default *val* =0.05). |
| <span class="table-cell-nowrap">/CDFF = *func*</span> | Specifies a user function expressing the cumulative distribution function. See Details. |
| <span class="table-cell-nowrap">/Q</span> | No results printed in the history area. |
| <span class="table-cell-nowrap">/T = *k*</span> | Displays results in a table. *k* specifies the table behavior when it is closed. |
|  |<table class="nested-table"><tbody><tr><td>*k*&nbsp;=0:</td><td>Normal with dialog (default).</td></tr><tr><td>*k*&nbsp;=1:</td><td>Kills with no dialog.</td></tr><tr><td>*k*&nbsp;=2:</td><td>Disables killing.</td></tr></tbody></table>
| <span class="table-cell-nowrap">/Z</span> | Ignores errors. V_flag will be set to -1 for any error and to zero otherwise. |

### *Details* {#details}
The Kolmogorov-Smirnov (KS) goodness-of-fit test applies only to continuous distributions and cases where the compared distribution (expressed as a user function) is completely specified without estimating parameters from the data. It compares the cumulative distribution function (CDF) of two distributions and sets the test statistic D to the largest difference between the CDFs. Because CDFs are in the range [0,1], D is also bound by this range.

When specifying the distributions with two waves, StatsKSTest first sorts the data in the waves and then computes the CDFs and D. You can also specify one of the distributions with a user function. For example, the following function tests if the data in *srcWave* is normally distributed with zero mean and stdv=5:

```igor
Function GetUserCDF(inX) : CDFFunc
	Variable inX
	return StatsNormalCDF(inX,0,5)
End
```

The ": CDFFunc" designation, which requires Igor 7 or later, tells Igor to make the function accessible from the Kolmogorov-Smirnov Test dialog.

Outputs are the number of elements, the KS statistic D, and the critical value. When both distributions are specified by waves, the number of elements is the weighted value (n1*n2)/(n1+n2).

### *References* {#references}
Critical values are based on:

Birnbaum, Z. W., and Fred H. Tingey, One-sided confidence contours for probability distribution functions, *The Annals of Mathematical Statistics*, *22*, 592-596, 1951.

A statistically more powerful modification of the classic KS test can be found in:

Khamis, H.J., The two-stage delta-corrected Kolmogorov-Smirnov test, *Journal of Applied Statistics*, *27*, 439-450, 2000.

StatsKSTest implements the original KS test. The difficulty in implementing the modified tests for all the cases defined by Stephens is in obtaining the critical values which have to be derived by time consuming Monte-Carlo simulations.

Critiques can be found in:

D'Agostino, R.B., and M. Stephens, eds., *Goodness-Of-Fit Techniques*, Marcel Dekker, New York, 1986.

NIST/SEMATECH, Kolmogorov-Smirnov Goodness-of-Fit Test, in *NIST/SEMATECH e-Handbook of Statistical Methods*, [http://www.itl.nist.gov/div898/handbook/eda/section3/eda35g.htm](http://www.itl.nist.gov/div898/handbook/eda/section3/eda35g.htm), 2005.

### *See Also* {#see-also}
[Statistical Analysis](/igorpro/analysis/statistics.md), [StatsJBTest](/igorpro/commands/statsjbtest.md), [WaveStats](/igorpro/commands/wavestats.md), [StatsCircularMoments](/igorpro/commands/statscircularmoments.md)