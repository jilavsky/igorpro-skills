---
description: "The FindPeak operation searches for a minimum or maximum by analyzing the smoothed first and second derivatives of the named wave."
slug: /commands/findpeak
---

<div className="command-signature">

## <strong>FindPeak</strong>  [/B=<em>box</em> /I/M=<em>minAmp</em> /N/P/Q/R=(<em>startX</em>,<em>endX</em> )] <em>waveName</em> {#findpeak}

</div>

The FindPeak operation searches for a minimum or maximum by analyzing the smoothed first and second derivatives of the named wave. Information about the peak position, amplitude, and width are returned in the output variables.

### *Flags* {#flags}
Some of the flags have the same meaning as for the FindLevel operation.


|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/B = *box*</span> | Sets box size for sliding average. |
| <span class="table-cell-nowrap">/I</span> | Modify the search criteria to accommodate impulses (peaks of one sample) by requiring only one value to exceed *minLevel*. |
|  | The default criteria requires that two successive values exceed *minLevel* for a peak to be found (or two successive values be less than the /M level when searching for negative peaks). |
|  | Impulses can also be found by omitting *minLevel*, in which case /I is superfluous. |
| <span class="table-cell-nowrap">/M = *minLevel*</span> | Defines minimum level of a peak. /N changes this to maximum level (see Details). |
| <span class="table-cell-nowrap">/N</span> | Searches for a negative peak (minimum) rather then a positive peak (maximum). |
| <span class="table-cell-nowrap">/P</span> | Location output variables (see below) are reported in terms of (floating point) point numbers. If /P is omitted, they are reported as X values. |
| <span class="table-cell-nowrap">/Q</span> | Doesn't print to history and doesn't abort if no peak is found. |
| <span class="table-cell-nowrap">/R = (*startX*,*endX* )</span> | Specifies X range and direction for search. |
| <span class="table-cell-nowrap">/R = [*startP*,*endP* ]</span> | Specifies point range and direction for search. |

FindPeak sets the following variables:


|  |  |
| --- | --- |
| V_flag | Set only when using the /Q flag. |
|  |<table class="nested-table"><tbody><tr><td>0:</td><td>Peak was found.</td></tr></tbody></table>
|  | Any nonzero value means the peak was not found. |
| V_LeadingEdgeLoc | Set to the interpolated location of the peak edge closest to *startX*  or *startP*. If you use the /P flag, V_LeadingEdgeLoc is a point number rather than to an X value. If the edge was not found, this value is NaN. |
| V_PeakLoc | Set to the interpolated X value at which the peak was found. If you use the /P flag, FindPeak sets V_PeakLoc to a point number rather than to an X value. Set to NaN if the peak wasn't found. |
| V_PeakVal | Set to the *approximate* Y value of the found peak. If the peak was not found, this value is NaN (Not a Number). |
| V_PeakWidth | Set to the interpolated peak width. If you use the /P flag, V_PeakWidth is expressed in point numbers rather than as an X value. V_PeakWidth is never negative. If either peak edge was not found, this value is NaN. |
| V_TrailingEdgeLoc | Set to the interpolated location of the peak edge closest to *endX* or *endP*. If you use the /P flag, V_TrailingEdgeLoc is a point number rather than to an X value. If the edge was not found, this value is NaN. |

### *Details* {#details}
FindPeak computes the sliding average of the input wave using the BoxSmooth algorithm with the *box* parameter. The peak center is found where the derivative of this smoothed result crosses zero. The peak edges are found where the second derivative of the smoothed result crosses zero. Linear interpolation of the derivatives is used to more precisely locate the center and edges. The peak value is simply the greater of the two unsmoothed values surrounding the peak center (if /N, then the lesser value).

FindPeak is not a high-accuracy measurement routine; it is intended as a simple peak-finder. Use the [PulseStats](/igorpro/commands/pulsestats.md) operation for more precise statistics.

Without /M, a peak is found where the derivative crosses zero, regardless of the peak height.

If you use the /M=*minLevel* flag, FindPeak ignores peaks that are lower than *minLevel* (i.e., the Y value of a found peak will exceed *minLevel* ) in the box-smoothed input wave. If /N is also specified (search for minimum), FindPeak ignores peaks whose amplitude is greater than *minLevel* (i.e., the Y value of a found peak will be *less* than *minLevel* ).

Without /I, a peak must have two successive values that exceed *minLevel*. Use /I when you are searching for peaks that may have only one value exceeding *minLevel*.

The search for the peak begins at *startX* (or the first point of the wave if /R is not specified), and ends at *endX* (or the last point of the wave if no /R). Searching backwards is permitted, and exchanges the values of V_LeadingEdgeLoc and V_TrailingEdgeLoc.

A simple automatic peak-finder is implemented in the "Peak Autofind.ipf" procedure file which is used in the Multipeak Fitting package. See Multipeak Fitting.

The FindPeak operation is not multidimensional aware. See [Multidimensional Waves](/igorpro/igor-basics/multidimensional-waves.md), particularly [Analysis on Multidimensional Waves](/igorpro/igor-basics/multidimensional-waves.md#analysis-on-multidimensional-waves) for details.

### *See Also* {#see-also}
[PulseStats](/igorpro/commands/pulsestats.md)

[FindLevel](/igorpro/commands/findlevel.md) for details about the /B, /P, /Q, and /R flag values.