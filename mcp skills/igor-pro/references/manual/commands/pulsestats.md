---
description: "The PulseStats operation produces simple statistics on a region of the named wave that is expected to contain three edges as shown below."
slug: /commands/pulsestats
---

<div className="command-signature">

## <strong>PulseStats</strong>  [/A=<em>n</em> /B=<em>box</em> /F=<em>f</em>  /L=(<em>startLevel</em>, <em>endLevel</em> )/M=<em>dx</em> /P/Q /R=(<em>startX</em>,<em>endX</em> )/T=<em>dx</em> ] <em>waveName</em> {#pulsestats}

</div>

The PulseStats operation produces simple statistics on a region of the named wave that is expected to contain three edges as shown below. If more than three edges exist, PulseStats works on the first three edges it finds.

<img src="Images/PulseStats/PulseStats_1.png" width="100%"/>

PulseStats handles two other cases in which there are only two edges or one edge.

<img src="Images/PulseStats/PulseStats_3.png" width="100%"/>



<img src="Images/PulseStats/PulseStats_5.png" width="100%"/>

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/A = *n*</span> | Automatically determines *startLevel* and *endLevel* by averaging *n* points centered at *startX* and *endX*. This does not work in case 2 which requires that you use the /L flag. Default is /A=1. |
| <span class="table-cell-nowrap">/B = *box*</span> | Sets box size for sliding average. This should be an odd number. If /B=*box* is omitted or *box* equals 1, no averaging is done. |
| <span class="table-cell-nowrap">/F = *f*</span> | Specifies levels 1, 2 and 3 as a fraction of (*endLevel*-*startLevel* ): |
|  | level1 = level2 = level3 = *f* \* (*endLevel* -*startLevel* )+*startLevel* |
|  | *f* must be between 0 and 1. The default value is 0.5 which sets the levels to mid-way between the base levels. |
| <span class="table-cell-nowrap">/L = (*startLevel*, *endLevel* )</span> |  |
|  | Sets *startLevel* and *endLevel* explicitly. |
| <span class="table-cell-nowrap">/M = *dx*</span> | Sets minimum edge width. Once an edge is found, the search for the next edge starts *dx* units beyond the found edge. Default *dx* is 0. |
| <span class="table-cell-nowrap">/P</span> | Output edge locations (see below) are set in terms of point number. If /P is omitted, edge locations are set in terms of X values. |
| <span class="table-cell-nowrap">/Q</span> | Prevents results from being printed in history and prevents error if edge is not found. |
| <span class="table-cell-nowrap">/R = (*startX*,*endX* )</span> | Specifies an x range of the wave to search. You may exchange *startX* and *endX* to reverse the search direction. |
| <span class="table-cell-nowrap">/R = [*startP*,*endP* ]</span> | Specifies a point range of the wave to search. You may exchange *startP* and *endP* to reverse the search direction. |
|  | If you specify the range as /R=[*startP* ] then the end of the range is taken as the end of the wave. If /R is omitted, the entire wave is searched. |
| <span class="table-cell-nowrap">/T = *dx*</span> | Forces search in two directions for a possibly more accurate result. *dx* controls where the second search starts. |

### *Details* {#details}
The /B=box, /T=dx, /P and /Q flags behave the same as for the FindLevel operation.

PulseStats considers a region of the input wave between two X locations, called *startX* and *endX*. *startX* and *endX* are set by the /R=(*startX*,*endX* ) flag. If this flag is missing, *startX* and *endX* default to the start and end of the entire wave.

The *startLevel* and *endLevel* values define the base levels of the pulse. You can explicitly set these levels with the /L=(*startLevel*, *endLevel* ) flag or you can let PulseStats find the base levels for you by using the /A=*n* flag. With this flag, PulseStats determines *startLevel* and *endLevel* by averaging *n* points centered at *startX* and at *endX*. In case 2, you must use /L=(*startLevel*, *endLevel* ) since *startLevel* is not at point 0.

Given *startLevel* and *endLevel* and an *f*  value (which you can set with the /F=*f* flag), PulseStats computes level1, level2 and level3 which are always equal. With the default *f* value of 0.5, level1 is mid-way between *startLevel* and *endLevel*.

With these levels defined, PulseStats searches the wave from *startX* to *endX* looking for one, two or three level crossings. PulseStats sets the following variables:


|  |  |
| --- | --- |
| V_flag |<table class="nested-table"><tbody><tr><td>0:</td><td>Found all three level crossings.</td></tr><tr><td>1:</td><td>Found one or two level crossings.</td></tr><tr><td>2:</td><td>No level crossings.</td></tr></tbody></table>
| V_PulseLoc1 | X location of level1. |
| V_PulseLoc2 | X location of level2. |
| V_PulseLoc3 | X location of level3. |
| V_PulseLvl0 | startLevel value. |
| V_PulseLvl123 | level1 value that is the same as level2 and level3. |
| V_PulseLvl4 | endLevel value. |
| V_PulseAmp4_0 | Pulse amplitude (endLevel - startLevel). |
| V_PulseWidth2_1 | Left pulse width (x distance between points 2 and 1). |
| V_PulseWidth3_2 | Right pulse width (x distance between points 3 and 2). |
| V_PulseWidth3_1 | Pulse period (x distance between point 3 and point 1). |
| V_PulsePolarity | Trend of the edge at point 1 (-1 if decreasing, +1 if increasing). |



X locations and distances are in terms of the X scaling of the source wave, unless you use the /P flag in which case they are in terms of point number.

If any level crossings are missing then PulseStats sets the associated variables to NaN (Not a Number).

If one crossing is missing, variables depending on point 3 are set to NaN.

If two crossings are missing, variables depending on points 2 and 3 are set to NaN.

If all crossings are missing, variables depending on points 1, 2, and 3 are set to NaN.

You can use the numtype function to test a variable to see if it is NaN.

The PulseStats operation is not multidimensional aware. See [Multidimensional Waves](/igorpro/igor-basics/multidimensional-waves.md), particularly [Analysis on Multidimensional Waves](/igorpro/igor-basics/multidimensional-waves.md#analysis-on-multidimensional-waves) for details.

### *See Also* {#see-also}
[FindLevel](/igorpro/commands/findlevel.md) about the /B=*box*, /T=*dx*, /P and /Q flags.

[EdgeStats](/igorpro/commands/edgestats.md), [numtype](/igorpro/commands/numtype.md)