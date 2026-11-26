---
description: "The StatsResample operation resamples srcWave by drawing (with replacement) numPoints values from srcWave and storing them in the output wave W_Resampled or…"
slug: /commands/statsresample
---

<div className="command-signature">

## <strong>StatsResample</strong>  /N=<em>numPoints</em> [ /ITER=<em>n</em>  /JCKN=<em>ufunc</em>  /K /Q /SQ=<em>m</em>  /WS=<em>m</em>  /Z ] <em>srcWave</em> {#statsresample}

</div>

The StatsResample operation resamples *srcWave* by drawing (with replacement) *numPoints* values from *srcWave* and storing them in the output wave W_Resampled or M_Resampled if /MC is used. You can iterate the process and compute various statistics on the data samples.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/DSTJ = *jkWave*</span> | Specify the destination wave for the Jack-Knife statistics.  If you do not specify this flag, the operation saves this output in the wave W_JackKnifeStats in the current data folder. |
|  | This flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/DSTR = *rWave*</span> | Specify the destination wave for the raw samples.  If you do not specify this flag, the operation saves the output in the wave W_Resampled in the current data folder.  The wave will have the same number of columns as the number of iterations.  Note that various flags can, as a side effect, prohibit the creation of this wave. |
|  | This flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/DSTQ = *qWave*</span> | Specify the destination wave for the results of StatsQuantilesTest applied to the resampled data.  If you do not specify this flag, the operation saves the results in the wave M_StatsQuantilesSamples in the current data folder.  The wave has the same number of columns as the number of iterations.  Note that various flags can, as a side effect, prohibit the creation of this wave. |
|  | This flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/DSTW = *wWave*</span> | Specify the destination wave for the results of WaveStats applied to the resampled data.  If you do not specify this flag, the operation saves these results in the wave M_WaveStatsSamples in the current data folder.  The wave has the same number of columns as the number of iterations. |
|  | This flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/FREE</span> | Creates all user-specified destination waves as free waves. |
|  | /FREE is allowed only in functions, and only if the destination waves are simple names or wave reference structure fields. |
|  | See [Free Waves](/igorpro/programming/programming.md#free-waves) for more discussion. |
|  | The /FREE flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/ITER = *n*</span> | Repeats the resampling for *n* iterations, which is useful only when combined with /WS or /SQ. |
|  | The /ITER flag is ignored by the Jack-Knife analysis (/JCKN). |
| <span class="table-cell-nowrap">/JCKN = *ufunc*</span> | Performs Jack-Knife analysis. |
|  | *ufunc* is a user function of the format: |
|  | <code class="igor">Function ufunc(inWave)&#10;	wave inWave&#10;	//... compute some statistic for inWave&#10;	return someValue&#10;End</code> |
|  | The results are stored in the wave W_JackKnifeStats in the current data folder. Use |
|  | <code class="igor">Edit W_JackKnifeStats.ld</code> |
|  | to display the wave with dimension labels. |
|  | In the Jack-Knife method the operation runs N iterations where N is the number of points in srcWave. In each iteration the opeation calls the user-defined function ufunc(inWave) passing it an internal wave which contains (N-1) samples from srcWave. The function computes some user-defined statistic, say "Z", and stores it in inWave. At the end of iterations the operation uses the Z values in inWave to compute various Jack-Knife estimates. The standard estimator is defined as: |
|  | $$ \displaystyle Z=\operatorname{ufunc}({srcWave}) . $$ |
|  | The Jack-Knife estimator is simply: |
|  | $$ \displaystyle \hat{z}=\frac{1}{n} \sum_{i=1}^{n} z_{i} . $$ |
|  | The Jack-Knife t-estimator is slightly less biased. It is given by: |
|  | $$ \displaystyle t=n Z-(n-1) \hat{z}, $$ |
|  | The estimate of the standard error is given by: |
|  | $$ \displaystyle \hat{\sigma}_{\hat{z}}=\sqrt{\frac{n-1}{n} \sum_{i=1}^{n}\left(z_{i}-\hat{z}\right)^{2}} . $$ |
|  | The Jack-Knife analysis ignores the /N and /ITER flags. The number of points and the number of iterations are determined by the number of points in *srcWave*. |
|  | This flag is incompatible with the flags /ITER /K /MC /SQ and /WS. |
| <span class="table-cell-nowrap">/K</span> | Kills W_Resampled after passing it to WaveStats. When /ITER is used, W_Resampled is not saved. |
| <span class="table-cell-nowrap">/MC</span> | Use this flag when you want to sample random (complete) rows from a multi-column 2D *srcWave*. The combination of /N=n with /MC results in the wave M_Resampled in the current data folder. M_Resampled will have n rows, the same number of columns and the same data type as *srcWave*. |
| <span class="table-cell-nowrap">/N = *numPoints*</span> | Specifies the number of points sampled from *srcWave*. |
|  | The /N flag is ignored by the Jack-Knife analysis (/JCKN). |
| <span class="table-cell-nowrap">/Q</span> | No information printed in the history area. |
| <span class="table-cell-nowrap">/SQ = *m*</span> | Uses [StatsQuantiles](/igorpro/commands/statsquantiles.md) to compute the data quartiles. The methods are: |
|  |<table class="nested-table"><tbody><tr><td>*m*&nbsp;=0:</td><td>Tukey (default).</td></tr><tr><td>*m*&nbsp;=1:</td><td>Minitab.</td></tr><tr><td>*m*&nbsp;=2:</td><td>Moore and McCabe.</td></tr><tr><td>*m*&nbsp;=3:</td><td>Mendenhall and Sincich.</td></tr></tbody></table>
|  | See Details for information about how the results are stored. |
|  | The default trim value is 25%. |
| <span class="table-cell-nowrap">/WS = *m*</span> | Uses the [WaveStats](/igorpro/commands/wavestats.md) operation to calculate data statistics. |
|  |<table class="nested-table"><tbody><tr><td>*m*&nbsp;=0:</td><td>Creates a new wave containing the samples (default).</td></tr><tr><td>*m*&nbsp;=1:</td><td>Creates the new wave and passes it to WaveStats/Q/M=1.</td></tr><tr><td>*m*&nbsp;=2:</td><td>Creates the new wave and passes it to WaveStats/Q/M=2.</td></tr></tbody></table>
|  | See Details for information about how the results are stored. |
| <span class="table-cell-nowrap">/Z</span> | Ignores any errors. |

### *Details* {#details}
StatsResample can perform Bootstrap Analysis, permutations tests, and Monte-Carlo simulations. It draws the specified number of data points (with replacement) from *srcWave* and places them in a destination wave W_Resampled.

Specify /WS or /SQ to use the [WaveStats](/igorpro/commands/wavestats.md) or [StatsQuantiles](/igorpro/commands/statsquantiles.md) operations, respectively, to compute results directly from the data. StatsResample normally creates the wave W_Resampled and, optionally, the M_WaveStats and W_StatsQuantiles waves. Both options also create various V_ variables described below. If you use more than one iteration, StatsResample creates instead the waves M_WaveStatsSamples and M_StatsQuantilesSamples for the results.

M_WaveStatsSamples (with /WS) contains a column for each iteration. Each column is equivalent to the contents of M_WaveStats for that iteration. You can use the command


```igor
Edit M_WaveStatsSamples.ld
```

to display the results in a table using row labels, and, for example, to display a graph of the rms of the samples as a function of iteration number execute:


```igor
Display M_WaveStatsSamples[5][]
```

M_StatsQuantilesSamples (with /SQ) contains a column for each iteration. Each column consists of the contents of W_StatsQuantiles for the corresponding data. Here again you can execute the command


```igor
Edit M_StatsQuantilesSamples.ld
```

to display the wave in a table using row labels. To display a graph of the median as a function of iteration execute:


```igor
Display M_statsQuantilesSamples[2][]
```

### *Output Variables* {#output-variables}
StatsResample creates the following variables: V_Median, V_Q25, V_Q75, V_IQR, V_min, V_max, V_numNaNs, V_numINFs, V_avg, V_sdev, V_rms, V_adev, V_skew, V_kurt, and V_Sum.

These variables are valid only if you use either /SQ or /WS, but not both, and only if you do not use /ITER. Unused variables are set to NaN.

If you use /SQ the operation sets V_Median, V_Q25, V_Q75, V_IQR, V_min, and V_max.

If you use /WS the operation sets V_min, V_max, V_numNaNs, V_numINFs, V_avg, V_sdev, V_rms, V_adev, V_skew, V_kurt, and V_Sum.

### *See Also* {#see-also}
[Statistical Analysis](/igorpro/analysis/statistics.md), [StatsSample](/igorpro/commands/statssample.md), [WaveStats](/igorpro/commands/wavestats.md), [StatsQuantiles](/igorpro/commands/statsquantiles.md)