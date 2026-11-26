---
description: "The StatsLinearRegression operation performs regression analysis on the input wave(s)."
slug: /commands/statslinearregression
---

<div className="command-signature">

## <strong>StatsLinearRegression</strong>  [/ALPH=<em>alpha</em> /T=<em>k</em> /Z/Q/WSTR=<em>strList</em> /BCIW/BPIW/TUK/DET=<em>index</em> ] [<em>wave0</em>, <em>wave1</em>,...] {#statslinearregression}

</div>

The StatsLinearRegression operation performs regression analysis on the input wave(s). Output is to the W_StatsLinearRegression wave in the current data folder or optionally to a table. Additionally, the M_DunnettMCElevations, M_TukeyMCSlopes, and M_TukeyMCElevations waves may be created as specified.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/ALPH = *val*</span> | Sets the significance level (default *val* =0.05). |
| <span class="table-cell-nowrap">/B = *beta0*</span> | Tests the hypothesis that the slope *b* = *beta0* (default is 0). The results are expressed by the t-statistic, which can be compared with the tc value for the two-tailed test. Get the critical value for a one-tailed test using `StatsStudentCDF(1-alpha,N-2)`. It does not work with /MYVW. |
| <span class="table-cell-nowrap">/BCIW</span> | Computes two confidence interval waves for the high side and the low side of the confidence interval. The new waves are named with _CH and _CL suffixes respectively appended to the Y wave name and are created in the current data folder. For multiple runs a numeric suffix will also be appended to the names. |
| <span class="table-cell-nowrap">/BPIW[ = *mAdditional* ]</span> |  |
|  | Computes prediction interval waves for the high side and the low side of the confidence interval on a single additional measurement (default). Use *mAdditional* to specify additional measurements. The new waves are named with _PH and _PL suffixes respectively appended to the Y wave name and are created in the current data folder. For multiple runs a numeric suffix will also be appended to the names. |
| <span class="table-cell-nowrap">/DEST = *lgWave*</span> | Specify the destination wave for the linear regression results.  If you do not use this flag, the operation saves this output in the wave W_StatsLinearRegression in the current data folder. |
|  | This flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/DET = *controlIndex*</span> |  |
|  | Performs Dunnett's multicomparison test for the elevations. The test requires more than two Y waves for regression, the test for the slopes should not reject the equal slope hypothesis, and the test for the elevations should reject the equal elevation hypothesis. *controlIndex* is the zero-based index of the Y wave representing the control (X waves do not count in the index specification). The test compares the elevation of every Y wave with the specified control. |
|  | Output is to the M_DunnettMCElevations wave in the current data folder or optionally to a table. For every Y wave and control Y wave combination, the results include SE, q, q' (shown as qp), and the conclusion with 1 to accept the hypothesis of equal elevations or 0 to reject it. Use /TAIL to determine the critical value and the sense of the test. If you use /TUK you will also get the Tukey test for the set of elevations. |
| <span class="table-cell-nowrap">/DSDE = *deWave*</span> | Specify the destination wave for the Dunnett's multicomparison test for the elevations (/DET). If you do not use this flag, the operation saves this output in the wave M_DunnettMCElevations in the current data folder. |
|  | This flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/DSTE = *tWave*</span> | Specify the destination wave for Tukey-type multiple regressions test for the elevations (/TUK). If you do not use this flag, the operation saves this output in the wave M_TukeyMCElevations in the current data folder. Note that the wave is not saved if the hypothesis of equal slopes can't be rejected (i.e., the wave is saved only if the slopes are different.) |
|  | This flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/DSTS = *sWave*</span> | Specify the destination wave for Tukey-type multiple regressions test for the elevations (/TUK).  If you do not use this flag the operation saves this output in the wave M_TukeyMCElevations in the current data folder. |
|  | This flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/FREE</span> | Creates all user-specified destination waves as free waves. |
|  | /FREE is allowed only in functions, and only if the destination waves are simple names or wave reference structure fields. |
|  | See [Free Waves](/igorpro/programming/programming.md#free-waves) for more discussion. |
|  | The /FREE flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/MYVW = {*xWave*, *yWave* }</span> |  |
|  | Specifies that the input consists of multiple Y values for each X value. It ignores all other inputs and the results are appropriate only for multiple Y values at each X point. |
|  | *yWave* is a 2D wave of values arranged in columns. Use NaNs for padding where rows do not have the same number of entries as others. It will use the X scaling of *yWave* when *xWave* is null, /MYVW={*,yWave}. |
|  | It first tests the hypothesis (H<sub>0</sub>) that the population regression is linear in an analysis of variance calculation. It generates results 1-7 (see ***Details***) as well as: Among Groups SS, Among Groups DF, Within Groups SS, Within Groups DF, Deviations from Linearity SS, Deviations from Linearity DF, F statistic defined by the ratio of Deviation from Linearity MS to Within Groups MS, and the critical value Fc. |
|  | Next, it tests the hypothesis that the slope beta=0. If the original H0 was accepted, the new F statistic=regressionMS/residualMS. Otherwise the with the critical F=regressionMS/WithinGroupsMS with a corresponding critical value. Finally, it reports the values of the coefficient of determination r2 and the standard error of the estimate S<sub>YX</sub>. |
| <span class="table-cell-nowrap">/PAIR</span> | Specifies that the input waves are XY pairs, where each pair must be an X wave followed by a Y wave. |
| <span class="table-cell-nowrap">/Q</span> | No results printed in the history area. |
| <span class="table-cell-nowrap">/RTO</span> | Reflects the regression through the origin. |
| <span class="table-cell-nowrap">/T = *k*</span> | Displays results in a table. *k* specifies the table behavior when it is closed. |
|  |<table class="nested-table"><tbody><tr><td>*k*&nbsp;=0:</td><td>Normal with dialog (default).</td></tr><tr><td>*k*&nbsp;=1:</td><td>Kills with no dialog.</td></tr><tr><td>*k*&nbsp;=2:</td><td>Disables killing.</td></tr></tbody></table>
| <span class="table-cell-nowrap">/TAIL = *tCode*</span> | Sets the sense of the test when applying Dunnett's test (see /DET). *tCode* is 1 or 2 for a one-tail critical value and 4 for a two-tail critical value. |
| <span class="table-cell-nowrap">/TUK</span> | Performs a Tukey-type test on multiple regressions on two or more Y waves. There are two possible Tukey-type tests: |
|  | The first is performed if the hypothesis of equal slopes is rejected. The operation then compares all combinations of two Y waves to identify if some of the waves have equal slopes. Output is to the M_TukeyMCSlopes wave in the current data folder or optionally to a table.  For every Y wave pair, the results include the difference between slopes (absolute value), q, the critical value qc, and the conclusion set to 1 for accepting the equality of the pair of slopes or 0 for rejecting the hypothesis. |
|  | The second Tukey-type test is performed if all the slopes are the same, but the elevations are not. The test (see /DET) compares all possible pairs of elevations to determine which satisfy the hypothesis of equality. Output is to the M_TukeyMCElevations wave in the current data folder. |
|  | <div><Admonition type="note"><p>When the slopes are equal, the wave M_TukeyMCSlopes is not created, so you should make sure that such a wave or the destination specified by /DSTS are not left over from previous executions of the operation. Similarly, the wave M_TukeyMCElevations or the destination specified by /DSTE should be cleared before executing the operation with this flag.</p></Admonition></div> |
| <span class="table-cell-nowrap">/WSTR = *waveListString*</span> |  |
|  | Specifies a string containing a semicolon-separated list of waves that contain sample data. Use *waveListString* instead of listing each wave after the flags. |
| <span class="table-cell-nowrap">/Z</span> | Ignores errors. |

### *Details* {#details}
Inputs may consist of Y waves or XY wave pairs. If X data are not used, the X values are inferred from the Y wave scaling. For multiple waves where only some have pairs, use the /PAIR flag and enter \* in each place where the X values should be computed.

For each input StatsLinearRegression calculates:


1.	Least squares regression line y=a+b*x.
2.	Mean value of X: xBar.
3.	Mean value of Y: yBar.
4.	Sum of the squares (x<sub>i</sub>-xBar)<sup>2</sup>.
5.	Sum of the squares (y<sub>i</sub>-yBar)<sup>2</sup>.
6.	Sum of the product (x<sub>i</sub>y<sub>i</sub>-xyBar).
7.	Standard error of the estimate 
$$
\displaystyle S_{Y X}^{2}=\frac{\sum\left(Y_{i}-\hat{Y}_{i}\right)^{2}}{n-2} .
$$
<sub></sub>
8.	F statistic for the hypothesis beta=0.
9.	Critical F value Fc.
10.	Coefficient of determination r2.
11.	Standard error of the regression coefficient S<sub>b</sub>.
12.	t-statistic for the hypothesis beta=*beta0* , NaN if /B is not specified.
13.	Critical value tc for the t-statistic above (used to calculate L1 and L2).
14.	Lower confidence interval boundary (L1) for the regression coefficient.
15.	Upper confidence interval boundary (L2) for the regression coefficient.

The remaining parts of the operation depend on the number of Y-waves at the input.  The following results are stored in the wave W_LinearRegressionMC in the current data folder:

For two Y waves with the same slope, it computes a common slope (bc) and then tests the equality of the elevations (a). In both cases it computes a t-statistic and compares it with a critical value. If the elevations are also the same then it computes the common elevation (ac) and the pooled means of X and Y in (xp) and (yp).

For more than two Y waves it computes:

$$
\displaystyle A_{c}=\sum_{j=1}^{W} A_{j} ; \quad A_{j} \equiv \sum x_{i}^{2}=\sum_{i=0}^{n_{j}-1} X_{i}^{2}-\frac{1}{n_{j}}\left(\sum_{i=0}^{n_{j}-1} X_{i}\right)^{2}
$$

$$
\displaystyle B_{c}=\sum_{j=1}^{W} B_{j} ; \quad B_{j} \equiv \sum x y=\sum_{i=0}^{n_{j}-1} X Y-\frac{1}{n_{j}}\left(\sum_{i=0}^{n_{j}-1} X_{i}\right)\left(\sum_{i=0}^{n_{j}-1} Y_{i}\right)
$$

$$
\displaystyle C_{c}=\sum_{j=1}^{W} C_{j} ; \quad C_{j} \equiv \sum y^{2}=\sum_{i=0}^{n_{j}-1} Y_{i}^{2}-\frac{1}{n_{j}}\left(\sum_{i=0}^{n_{j}-1} Y_{i}\right)^{2}
$$

$$
\displaystyle S S p=\sum_{j=1}^{W} C_{j}-\frac{B_{j}^{2}}{A_{j}}
$$

$$
\displaystyle S S c=C c-\frac{B_{c}^{2}}{A_{c}^{2}}
$$

$$
S S t=\sum_{j=1}^{W} \sum_{i=0}^{n_{j}} Y_{j i}^{2}-\frac{1}{N}\left(\sum_{j=1}^{W} \sum_{i=0}^{n_{j}} Y_{j i}\right)^{2}-\frac{\displaystyle \left(\sum_{j=1}^{W} \sum_{i=0}^{n_{j}} X_{j i} Y_{j i}-\frac{1}{N}\left(\sum_{j=1}^{W} \sum_{i=0}^{n_{j}} X_{j i}\right)\left(\sum_{j=1}^{W} \sum_{i=0}^{n_{j}} Y_{j i}\right)\right)^{2}}{\displaystyle \sum_{j=1}^{W} \sum_{i=0}^{n_{j}} X_{j i}^{2}-\frac{1}{N}\left(\sum_{j=1}^{W} \sum_{i=0}^{n_{j}} X_{j i}\right)^{2}}
$$

$$
\displaystyle D F p=\sum_{j=1}^{W}\left(n_{i}-2\right)
$$

$$
\displaystyle D F t=\sum_{j=1}^{W} n_{i}-2
$$

Here *W* is the number of Y waves and 
$$
\displaystyle N=\sum_{j=1}^{W} n_{j}
$$
is the total number of data points in all Y waves.

The test statistic F for equality of slopes is given by:

$$
\displaystyle F=\left(\frac{S S c-S S p}{ { numWaves }-1}\right) / \frac{S S p}{D F p}.
$$

Fc is the corresponding critical value.

Output is to the W_LinearRegressionMC wave in the current data folder.

V_flag is set to -1 for any error and to zero otherwise.

S_waveNames is set to a semicolon separated-list of the names of the waves created by the operation.

### *References* {#references}
See, in particular, Chapter 18 of:

Zar, J.H., *Biostatistical Analysis*, 4th ed., 929 pp., Prentice Hall, Englewood Cliffs, New Jersey, 1999.

### *See Also* {#see-also}
[Statistical Analysis](/igorpro/analysis/statistics.md), [CurveFit](/igorpro/commands/curvefit.md)

### *Demos* {#demos}
[Open Linear Regression Demo.pxp](#igor-pxp/Examples/Statistics/Linear__Regression__Demo.pxp)