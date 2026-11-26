---
description: "The WaveStats operation computes several values associated with the named wave."
slug: /commands/wavestats
---

<div className="command-signature">

## <strong>WaveStats</strong>  [<em>flags</em>] <em>waveName</em> {#wavestats}

</div>

The WaveStats operation computes several values associated with the named wave.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/ALPH = *val*</span> | Sets the significance level for the confidence interval of the mean (default *val* =0.05). |
| <span class="table-cell-nowrap">/C = *method*</span> | Calculates statistics for complex waves only. Has no effect on real waves. |
|  | You can use *method* in various combinations to process the real, imaginary, magnitude, and phase of the wave. The result is stored in the wave M_WaveStats (see Details for format). |
|  |<table class="nested-table"><tbody><tr><td>*method*&nbsp;=0:</td><td>Default; the imaginary part of *waveName* is ignored. Use /W to also store statistics in M_WaveStats.</td></tr><tr><td>*method*&nbsp;=1:</td><td>Calculates statistics for real part of *waveName* and stores it in M_WaveStats.</td></tr><tr><td>*method*&nbsp;=2:</td><td>Calculates statistics for imaginary part of *waveName* and stores the result in M_WaveStats.</td></tr><tr><td>*method*&nbsp;=4:</td><td>Calculates statistics for magnitude of *waveName*,  i.e., sqrt(real^2 +imag^2), and stores the result in M_WaveStats.</td></tr><tr><td>*method*&nbsp;=8:</td><td>Calculate statistics for phase of *waveName* using atan2(imag,real).</td></tr></tbody></table>
|  | If you use a single *method* the results are stored both in M_WaveStats and in the standard variables (e.g., V_avg, etc.). If you specify a *method* that is a combination of more than one binary field then the variables reflect the results for the lowest chosen field and all results are stored in the wave M_WaveStats. |
|  | For example, if you use /C=12, the variables will be set for the statistics of the magnitude and M_WaveStats will contain columns corresponding to the magnitude and to the phase. |
|  | In this mode V_numInfs will always be zero. |
|  | <div><Admonition type="note"><p>If you invoke this operation and M_WaveStats already exists in the current data folder, it will be either overwritten or initialized to NaN according to the /C flag.</p></Admonition></div> |
| <span class="table-cell-nowrap">/CCL</span> | When computing per-column statistics using /PCST, /CCL tells Igor to copy the column dimension labels of the input to the corresponding columns of M_WaveStats. /CCL was added in Igor Pro 9.00. |
| <span class="table-cell-nowrap">/DEST = *wStats*</span> | Specify a destination wave for WaveStats in place of the default M_WaveStats.  Note that in order for the operation to create the destination wave, you must also specify the appropriate combination of /W and /C flags. |
|  | This flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/FREE</span> | Creates the user-specified destination wave as a free wave.  Note that this flag does not affect the default M_WaveStats or W_ZScores. |
|  | /FREE is allowed only in functions and only if the destination waves are simple names or wave reference structure fields. |
|  | See [Free Waves](/igorpro/programming/programming.md#free-waves) for more discussion. |
|  | The /FREE flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/M = *moment*</span> | Calculates statistical moments. |
|  |<table class="nested-table"><tbody><tr><td>*moment*&nbsp;=1:</td><td>Calculates the lower moments: V_avg, V_npnts, V_numInfs, V_numNaNs. Use it if you do not need the higher moments.</td></tr><tr><td>*moment*&nbsp;=2:</td><td>Default; calculates both the lower moments and the higher order quantities: V_sdev, V_rms, V_adev, V_skew, v_kurt.</td></tr></tbody></table>
| <span class="table-cell-nowrap">/P</span> | Causes WaveStats to set the location output variables in terms of unscaled index values instead of the default scaled index values. The location output variables are: |
|  | <code class="igor">V_minRowLoc, V_maxRowLoc, V_minColLoc, V_maxColLoc&#10;V_minLayerLoc, V_maxLayerLoc, V_minChunkLoc, V_maxChunkLoc</code> |
|  | For 1D waves, V_minRowLoc and V_maxRowLoc are always unscaled. |
|  | /P requires Igor Pro 8.03 or later. |
| <span class="table-cell-nowrap">/PCST</span> | Computes the statistics on a per-column basis for a real valued wave of two or more dimensions. The results are saved in the wave M_WaveStats which has the same number of columns, layers and chunks as the input wave and where the rows, designated by dimension labels, contain the standard WaveStats statistics. All the V_ variables are set to NaN. Note that this flag is not compatible with the flags /C, /R, /RMD. |
|  | The /PCST flag was added in Igor Pro 7.00. |
| <span class="table-cell-nowrap">/Q</span> | Prevents results from being printed in history. |
| <span class="table-cell-nowrap">/R = (*startX*,*endX* )</span> | Specifies an X range of the wave to evaluate. |
| <span class="table-cell-nowrap">/R = [*startP*,*endP* ]</span> | Specifies a point range of the wave to evaluate. |
|  | If you specify the range as /R=[*startP* ] then the end of the range is taken as the end of the wave. If /R is omitted, the entire wave is evaluated. |
| <span class="table-cell-nowrap">/RMD = [*firstRow* , *lastRow* ][*firstColumn* , *lastColumn* ][*firstLayer* , *lastLayer* ][*firstChunk* , *lastChunk* ]</span> |  |
|  | Designates a contiguous range of data in the source wave to which the operation is to be applied. This flag was added in Igor Pro 7.00. |
|  | You can include all higher dimensions by leaving off the corresponding brackets. For example: |
|  | <code class="igor">/RMD=[firstRow,lastRow]</code> |
|  | includes all available columns, layers and chunks. |
|  | You can use empty brackets to include all of a given dimension. For example: |
|  | <code class="igor">/RMD=[][firstColumn,lastColumn]</code> |
|  | means "all rows from firstColumn to lastColumn". |
|  | You can use a * to specify the end of any dimension. For example: |
|  | <code class="igor">/RMD=[firstRow,*]</code> |
|  | means "from firstRow through the last row". |
| <span class="table-cell-nowrap">/W[ = mode]</span> | If the optional mode is not used, the operation stores results in the various V_ variables.  For complex waves when /C is not specified, the statistics are computed for the real part only. |
|  |<table class="nested-table"><tbody><tr><td>*mode*=0:</td><td>The operation stores the results in the V_ variables only and prints them to the history (subject to /Q).  For complex waves, if /C is specified with a non-zero method, the operation creates the corresponding M_WaveStats wave.</td></tr><tr><td>*mode*=1:</td><td>The operation saves the results in both the V_ variables and in the wave M_WaveStats.</td></tr><tr><td>*mode*=2:</td><td>The operation stores the results only in M_WaveStats and does not print the V_ variables.  When executed from a user function, the variables are created but are not updated by the operation.</td></tr></tbody></table>
| <span class="table-cell-nowrap">/Z</span> | No error reporting. |
| <span class="table-cell-nowrap">/ZSCR</span> | Computes z scores |
|  | $$ \displaystyle z_{i}=\frac{Y_{i}-\bar{Y}}{\sigma}, $$ |
|  | which are saved in W_ZScores. |

### *Details* {#details}
WaveStats uses a two-pass algorithm to produce more accurate results than obtained by computing the binomial expansions of the third and fourth order moments.

WaveStats returns the statistics in the automatically created variables:


|  |  |
| --- | --- |
| V_npnts | Number of points in range excluding points whose value is NaN or INF. |
| V_numNans | Number of NaNs. |
| V_numINFs | Number of INFs. |
| V_avg | Average of data values. |
| V_sum | Sum of data values. |
| V_sdev | Standard deviation of data values, |
|  | $$ \displaystyle \sigma=\sqrt{\frac{\sum\left(Y_{i}-V\_avg\right)^{2}}{V\_npnts-1}} $$ |
|  | "Variance" is V_sdev<sup>2</sup>. |
| V_sem | Standard error of the mean $$ \displaystyle { sem }=\frac{\sigma}{\sqrt{V\_npnts}} $$<sub></sub> |
| V_rms | RMS of Y values $$ \displaystyle =\sqrt{\frac{1}{V\_npnts} \sum Y_{i}^{2}} $$<sub></sub> |
| V_adev | Average deviation $$ \displaystyle =\frac{1}{V\_npnts } \sum_{i=0}^{{V\_npts }-1}\left\|Y_{i}-\bar{Y}\right\| $$<sub></sub> |
| V_skew | Skewness $$ \displaystyle =\frac{1}{V\_npnts} \sum_{i=0}^{V\_npnts-1}\left(\frac{Y_{i}-\bar{Y}}{\sigma}\right)^{3} $$<sub></sub> |
| V_kurt | Kurtosis $$ \displaystyle =\left(\frac{1}{V\_npnts} \sum_{i=0}^{V\_npnts-1}\left(\frac{Y_{i}-\bar{Y}}{\sigma}\right)^{4}\right)-3 $$<sub></sub> |
| V_minloc | X location of minimum data value. |
| V_min | Minimum data value. |
| V_maxloc | X location of maximum data value. |
| V_max | Maximum data value. |
| V_minRowLoc | Row containing minimum data value. See /P above for further information. |
| V_maxRowLoc | Row containing maximum data value. See /P above for further information. |
| V_minColLoc | Column containing minimum data value (2D or higher waves). See /P above for further information. |
| V_maxColLoc | Column containing maximum data value (2D or higher waves). See /P above for further information. |
| V_minLayerLoc | Layer containing minimum data value (3D or higher waves). See /P above for further information. |
| V_maxLayerLoc | Layer containing maximum data value (3D or higher waves). See /P above for further information. |
| V_minChunkLoc | Chunk containing minimum data value (4D waves only). See /P above for further information. |
| V_maxChunkLoc | Chunk containing maximum data value (4D waves only). See /P above for further information. |
| V_startRow | The unscaled index of the first row included in calculating statistics. |
| V_endRow | The unscaled index of the last row included in calculating statistics. |
| V_startCol | The unscaled index of the first column included in calculating statistics. Set only when /RMD is used. |
| V_endCol | The unscaled index of the last column included in calculating statistics. Set only when /RMD is used. |
| V_startLayer | The unscaled index of the first layer included in calculating statistics. Set only when /RMD is used. |
| V_endLayer | The unscaled index of the last layer included in calculating statistics. Set only when /RMD is used. |
| V_startChunk | The unscaled index of the first chunk included in calculating statistics. Set only when /RMD is used. |
| V_endChunk | The unscaled index of the last chunk included in calculating statistics. Set only when /RMD is used. |

WaveStats prints the statistics in the history area unless /Q is specified. The various multidimensional min and max location variables will only print to the history area for waves having the appropriate dimensionality.

The format of the M_WaveStats wave is:

| Row | Statistic |
| --- | --- |
| 0 | numPoints |
| 1 | numNaNs |
| 2 | numInfs |
| 3 | avg |
| 4 | sdev |
| 5 | rms |
| 6 | adev |
| 7 | skew |
| 8 | kurt |
| 9 | minLoc |
| 10 | min |
| 11 | maxLoc |
| 12 | max |
| 13 | minRowLoc |
| 14 | minColLoc |
| 15 | minLayerLoc |
| 16 | minChunkLoc |
| 17 | maxRowLoc |
| 18 | maxColLoc |
| 19 | maxLayerLoc |
| 20 | maxChunkLoc |
| 21 | startRow |
| 22 | endRow |
| 23 | sum |
| 24 | meanL1 |
| 25 | meanL2 |
| 26 | sem |
| 27 | startCol |
| 28 | endCol |
| 29 | startLayer |
| 30 | endLayer |
| 31 | startChunk |
| 32 | endChunk |

meanL1 and meanL2 are the confidence intervals for the mean

$$
\displaystyle { MeanL } 1={V\_avg}-t_{\alpha, v} \frac{V\_sdev}{\sqrt{V\_npnts}},
$$
 and  
$$
\displaystyle { MeanL2 }={V\_avg}+t_{\alpha, v} \frac{{V\_sdev}}{\sqrt{{V\_npnts}}}
$$
<sub></sub>

where *t*<sub>a,v</sub>  is the critical value of the Student T distribution for *alpha* significance and degree of freedom *v* =*V_npnts* -1.

Use `Edit M_WaveStats.ld` to display the results in a table with dimension labels identifying each of the row statistics.

WaveStats is not entirely multidimensional aware. Even so, much of the information computed by WaveStats is useful. See [Multidimensional Waves](/igorpro/igor-basics/multidimensional-waves.md), particularly [Analysis on Multidimensional Waves](/igorpro/igor-basics/multidimensional-waves.md#analysis-on-multidimensional-waves) for details.

See the [ImageStats](/igorpro/commands/imagestats.md) operation for calculating wave statistics for regions in 2D matrix waves.

### *See Also* {#see-also}
See [Statistical Analysis](/igorpro/analysis/statistics.md) for details on other statistics.

See the [ImageStats](/igorpro/commands/imagestats.md) operation for calculating wave statistics for regions in 2D matrix waves.

See the [APMath](/igorpro/commands/apmath.md) operation if you require higher precision than provided by double-precision floating point.

[WaveMax](/igorpro/commands/wavemax.md), [WaveMin](/igorpro/commands/wavemin.md), [WaveMinAndMax](/igorpro/commands/waveminandmax.md), [mean](/igorpro/commands/mean.md), [median](/igorpro/commands/median.md), [Variance](/igorpro/commands/variance.md)