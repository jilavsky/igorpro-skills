---
description: "The FindLevel operation searches the named wave to find the X value at which the specified Y level is crossed."
slug: /commands/findlevel
---

<div className="command-signature">

## <strong>FindLevel</strong>  [/B=<em>box</em> /EDGE=<em>e</em> /P/Q/R=(<em>startX</em>,<em>endX</em> )/T=<em>dx</em> ] <em>waveName</em>, <em>level</em> {#findlevel}

</div>

The FindLevel operation searches the named wave to find the X value at which the specified Y *level*  is crossed.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/B = *box*</span> | Sets box size for sliding average. If /B=*box*  is omitted or *box*  equals 1, no averaging is done. If you specify an even box size then the next higher (odd) integer is used. If you use a box size greater than 1, FindLevel will be unable to find a level crossing that occurs in the first or last (*box*-1)/2 points of the wave since these points don't have enough neighbors for computing the derived average wave values. |
| <span class="table-cell-nowrap">/EDGE = *e*</span> | Specifies searches for either increasing or decreasing level crossing |
|  |<table class="nested-table"><tbody><tr><td>*e*&nbsp;=0:</td><td>Same as no /EDGE flag (searches for either increasing and decreasing level crossing).</td></tr><tr><td>*e*&nbsp;=1:</td><td>Searches only for crossing where the Y values are increasing as *level*  is crossed from wave start towards wave end.</td></tr><tr><td>*e*&nbsp;=2:</td><td>Searches only for crossing where the Y values are decreasing as *level*  is crossed from wave start towards wave end.</td></tr></tbody></table>
| <span class="table-cell-nowrap">/P</span> | Computes the X crossing location in terms of point number. If /P is omitted, the level crossing location is computed in terms of X values. |
| <span class="table-cell-nowrap">/Q</span> | Prevents results from being printed in history and prevents error if *level*  is not found. |
| <span class="table-cell-nowrap">/R = (*startX*,*endX*)</span> | Specifies an X range of the wave to search. You may exchange *startX*  and *endX*  to reverse the search direction. |
| <span class="table-cell-nowrap">/R = [*startP*,*endP*]</span> | Specifies a point range of the wave to search. You may exchange *startP*  and *endP*  to reverse the search direction. |
|  | If you specify the range as /R=[*startP*] then the end of the range is taken as the end of the wave. If /R is omitted, the entire wave is searched. |
| <span class="table-cell-nowrap">/T = *dx*</span> | Performs a second search after finding the initial level crossing. The second search starts *dx* units beyond the initial level crossing and looks back in the direction of the initial crossing. If FindLevel finds a second level crossing, it sets V_LevelX to the average of the initial and second crossings. Otherwise, it sets V_LevelX to the initial crossing. |

### *Details* {#details}
FindLevel scans through the wave comparing *level* to values derived from the Y values of the wave. Each derived value is a sliding average of the Y values.

FindLevel searches for two derived wave values that straddle *level*. If it finds these values it computes the X value at which *level* is located by linearly interpolating between the straddling Y values.

FindLevel does not locate values exactly equal to *level*; it locates transitions through *level*. See [BinarySearch](/igorpro/commands/binarysearch.md) for one method of locating exact values.

FindLevel reports its results by setting these variables:

|  |  |
| --- | --- |
| V_flag |<table class="nested-table"><tbody><tr><td>0:</td><td>*level* was found.</td></tr><tr><td>1:</td><td>*level* was not found.</td></tr></tbody></table>
| V_LevelX | The interpolated X value at which *level* was found, or the corresponding point number if /P is specified. |
| V_rising |<table class="nested-table"><tbody><tr><td>0:</td><td>Y values at the crossing are decreasing from wave start towards wave end.</td></tr><tr><td>1:</td><td>Y values at the crossing are increasing.</td></tr></tbody></table>

If you omit the /Q flag then FindLevel also reports its results by printing them in the history area.

If *level*  is not found, and if you omit the /Q flag, FindLevel generates an error which puts up an error alert and  halts execution of any command line or macro that is in progress.

V_LevelX is returned in terms of the X scaling of the named wave unless you use the /P flag, in which case it is in terms of point number.

### *FindLevel Handling of NaNs* {#findlevel-handling-of-nans}
In Igor Pro 8.00 and later, FindLevel handles NaN values differently than previous versions. Now if *level* falls between two non-NaN wave Y values with NaNs between them, those two Y values and their associated X scaling values are used to linearly interpolate the X location of the level crossing. Igor 7 and earlier fail to find a crossing and set V_LevelX to NaN.

For example:


```igor
// Prints 2.5 in Igor 8 or later, NaN in Igor 7 or before
Make/O wave0 = {0, 1, NaN, NaN, 4, 5}
FindLevel/Q wave0, 2.5; Print V_levelX
```

You can revert to the pre-Igor 8 behavior by executing:


```igor
SetIgorOption UseIP6FindLevel = 1
```

### *FindLevel  and Multidimensional Waves* {#findlevel-and-multidimensional-waves}
The FindLevel operation is not multidimensional aware. See [Multidimensional Waves](/igorpro/igor-basics/multidimensional-waves.md), particularly [Analysis on Multidimensional Waves](/igorpro/igor-basics/multidimensional-waves.md#analysis-on-multidimensional-waves) for details.

### *See Also* {#see-also}
[FindLevels](/igorpro/commands/findlevels.md), [FindValue](/igorpro/commands/findvalue.md), [BinarySearch](/igorpro/commands/binarysearch.md), [BinarySearchInterp](/igorpro/commands/binarysearchinterp.md), [EdgeStats](/igorpro/commands/edgestats.md), [PulseStats](/igorpro/commands/pulsestats.md)