---
description: "The EdgeStats operation produces simple statistics on a region of a wave that is expected to contain a single edge."
slug: /commands/edgestats
---

<div className="command-signature">

## <strong>EdgeStats</strong>  [/A=<em>avgPts</em> /B=<em>box</em> /F=<em>frac</em> /L=(<em>startLevel</em>, <em>endLevel</em> ) /P /Q /R=(<em>startX</em>, <em>endX</em> ) /T=<em>dx</em> ] <em>waveName</em> {#edgestats}

</div>

The EdgeStats operation produces simple statistics on a region of a wave that is expected to contain a single edge. If more than one edge exists, EdgeStats works on the first edge it finds.

<img src="Images/EdgeStats/EdgeStats_1.png" width="100%"/>

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/A = *avgPts*</span> | Determines  *startLevel*  and *endLevel*  automatically by averaging *avgPts*  points at centered at *startX*  and *endX*. Default is /A=1. |
| <span class="table-cell-nowrap">/B = *box*</span> | Sets box size for sliding average. This should be an odd number. If /B=*box* is omitted or *box* equals 1, no averaging is done. |
| <span class="table-cell-nowrap">/F = *frac*</span> | Specifies levels 1, 2 and 3 as a fraction of (*endLevel* -*startLevel* ): |
|  | level1 = *frac* \* (*endLevel* - *startLevel* ) + *startLevel* |
|  | level2 = 0.5 \* (*endLevel* - *startLevel* ) + *startLevel* |
|  | level3 = (1 - *frac* ) \* (*endLevel* - *startLevel* ) + *startLevel* |
|  | The default value for *frac*  is 0.1 which makes level1 the 10% level, level2 the 50% level and level3 the 90% level. |
|  | *frac* must be between 0 and 0.5. |
| <span class="table-cell-nowrap">/L = (*startLevel*, *endLevel*)</span> |  |
|  | Sets *startLevel*  and *endLevel*  explicitly. If omitted, they are determined automatically. See /A. |
| <span class="table-cell-nowrap">/P</span> | Output edge locations (see below) are returned in terms of point number. If /P is omitted, edge locations are returned in terms of X values. |
| <span class="table-cell-nowrap">/Q</span> | Prevents results from being printed in history and prevents error if edge is not found. |
| <span class="table-cell-nowrap">/R = (*startX*,*endX*)</span> | Specifies an x range of the wave to search. You may exchange *startX*  and *endX*  to reverse the search direction. |
| <span class="table-cell-nowrap">/R = [*startP*,*endP*]</span> | Specifies a point range of the wave to search. You may exchange *startP* and *endP* to reverse the search direction. If /R is omitted, the entire wave is searched. |
| <span class="table-cell-nowrap">/T = *dx*</span> | Forces search in two directions for a possibly more accurate result. *dx* controls where the second search starts. |

### *Details* {#details}
The /B=*box*, /T=*dx*, /P and /Q flags behave the same as for the FindLevel operation.

EdgeStats considers a region of the input wave between two X locations, called *startX* and *endX*. *startX* and *endX*  are set by the /R=(*startX*,*endX*) flag. If this flag is missing, *startX* and *endX* default to the start and end of the entire wave. *startX* can be greater than *endX* so that the search for an edge can proceed from the "right" to the "left".

The diagram above shows the default search direction, from the "left" (lower point numbers) of the wave toward the "right" (higher point numbers).

The *startLevel* and *endLevel* values define the base levels of the edge. You can explicitly set these levels with the /L=(*startLevel*, *endLevel*) flag or you can let EdgeStats find the base levels for you by using the /A=*avgPts* flag which averages points around *startX* and *endX*.

Given *startLevel* and *endLevel* and a *frac* value (see the /F=*frac*  flag) EdgeStats defines level1, level2 and level3 as shown in the diagram above. With the default *frac*  value of 0.1, level1 is the 10% point, level2 is the 50% point and level3 is the 90% point.

With these levels defined, EdgeStats searches the wave from *startX* to *endX* looking for level2. Having found it, it then searches for level1 and level3. It returns results via variables described below.

EdgeStats sets the following variables:


|  |  |
| --- | --- |
| V_flag |<table class="nested-table"><tbody><tr><td>0:</td><td>All three level crossings were found.</td></tr><tr><td>1:</td><td>One or two level crossings were found.</td></tr><tr><td>2:</td><td>No level crossings were found.</td></tr></tbody></table>
| V_EdgeLoc1 | X location at which level1 was found. |
| V_EdgeLoc2 | X location at which level2 was found. |
| V_EdgeLoc3 | X location at which level3 was found. |
| V_EdgeLvl0 | *startLevel* value. |
| V_EdgeLvl1 | level1 value. |
| V_EdgeLvl2 | level2 value. |
| V_EdgeLvl3 | level3 value. |
| V_EdgeLvl4 | *endLevel*  value. |
| V_EdgeAmp4_0 | Edge amplitude (*endLevel* - *startLevel* ) |
| V_EdgeDLoc3_1 | Edge width (x distance between point 1 and point 3) |
| V_EdgeSlope3_1 | Edge slope (straight line slope from point 1 to point 3) |

These X locations and distances are in terms of the X scaling of the named wave unless you use the /P flag, in which case they are in terms of point number.

The EdgeStats operation is not multidimensional aware. See [Multidimensional Waves](/igorpro/igor-basics/multidimensional-waves.md), particularly [Analysis on Multidimensional Waves](/igorpro/igor-basics/multidimensional-waves.md#analysis-on-multidimensional-waves) for details.

### *See Also* {#see-also}
[FindLevel](/igorpro/commands/findlevel.md) about the /B=*box*, /T=*dx*, /P and /Q flags, and [PulseStats](/igorpro/commands/pulsestats.md).