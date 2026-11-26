---
description: "FindAPeak locates the maximum or minimum of a peak by analyzing smoothed first and second derivatives."
slug: /commands/findapeak
---

<div className="command-signature">

## <strong>FindAPeak</strong>  [/B=<em>baseWaveName</em> ] <em>minamp</em>, <em>pol</em>, <em>box</em>, <em>peakWave</em> [ (<em>startX</em>,<em>endX</em> ) ] {#findapeak}

</div>

FindAPeak locates the maximum or minimum of a peak by analyzing smoothed first and second derivatives.

The FindAPeak operation is used primarily by the Igor Technical Note #20 and its variants. For most purposes, use the more flexible [FindPeak](/igorpro/commands/findpeak.md) operation instead of FindAPeak.

### *Parameters* {#parameters}
*minamp* is minimum amplitude ("threshold") of a peak. Use it to reject small or spurious peaks.

*pol* is the expected peak polarity. Specify 1 to search for a positive-going peak or 2 to search for a negative-going peak.

*box* is the number of peak values to include in the sliding average when smoothing the derivatives. If you specify an even number, the next-higher odd number is used.

*peakWave* specifies the wave containing the peak.

[*startX*,*endX* ] is an optional subrange to search in point numbers.

(*startX*,*endX* ) is an optional subrange to search in X values.

If you omit the subrange, *startX* defaults to the first point in *peakWave* and *endX* defaults to the last point in *peakWave*.

The search always with *startX* and ends at *endX*, regardless of whether *startX* is less than or greater than *endX*. You can use this to control the direction of the search.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/B = *baseWave*</span> | Specifies a base wave containing values to subtract from *peakWave* to compute the derived data which FindAPeak searches for peaks. |

### *Details* {#details}
FindAPeak creates a temporary smoothed version of *peakWave* and a temporary first derivative of the smoothed data. It scans through the first derivative for the first zero-crossing where the smoothed data exceeds the minimum amplitude as specified by *minamp*. The location of the zero-crossing is then more accurately determined by reverse linear interpolation. The smoothed second derivative is computed at that point to see if the peak is a positive-going or negative-going peak.

### *Output Variables* {#output-variables}
FindAPeak reports results through these output variables:


|  |  |
| --- | --- |
| V_Flag | 0 if a peak is found and to 1 if no peak is found. |
| V_peakX | The interpolated X value of the peak center. |
| V_peakP | The interpolated fractional point number of the peak center. |

### *See Also* {#see-also}
[FindPeak](/igorpro/commands/findpeak.md), [EstimatePeakSizes](/igorpro/commands/estimatepeaksizes.md)