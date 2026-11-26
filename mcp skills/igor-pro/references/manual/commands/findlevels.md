---
description: "The FindLevels operation searches the named wave to find one or more X values at which the specified Y level is crossed."
slug: /commands/findlevels
---

<div className="command-signature">

## <strong>FindLevels</strong>  [/B=<em>box</em> /D=<em>destWaveName</em> /DEST=<em>destWaveName</em> /EDGE=<em>e</em> /M=<em>minWidthX</em> /N=<em>maxLevels</em> /P/Q  /R=(<em>startX</em>,<em>endX</em>)/T=<em>dx</em>]<em>waveName</em>, <em>level</em> {#findlevels}

</div>

The FindLevels operation searches the named wave to find one or more X values at which the specified Y *level* is **crossed**.

To find where the wave is **equal** to a given value, use [FindValue](/igorpro/commands/findvalue.md) instead.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/B = *box*</span> | Sets box size for sliding average. See the [FindLevel](/igorpro/commands/findlevel.md) operation. |
| <span class="table-cell-nowrap">/D = *destWaveName*</span> | Specifies wave into which FindLevels is to store the level crossing values. If /D and /DEST are omitted, FindLevels creates a wave named W_FindLevels to store the level crossing values in. |
| <span class="table-cell-nowrap">/DEST = *destWaveName*</span> |  |
|  | Same as /D. Both /D and /DEST create a real wave reference for the destination wave in a user function. See [Automatic Creation of WAVE References](/igorpro/programming/programming.md#automatic-creation-of-wave-references) for details. |
| <span class="table-cell-nowrap">/EDGE = *e*</span> | Specifies searches for either increasing or decreasing level crossing |
|  |<table class="nested-table"><tbody><tr><td>*e*&nbsp;=0:</td><td>Same as no /EDGE flag (searches for either increasing and decreasing level crossing).</td></tr><tr><td>*e*&nbsp;=1:</td><td>Searches only for crossing where the Y values are increasing as *level* is crossed from wave start towards wave end.</td></tr><tr><td>*e*&nbsp;=2:</td><td>Searches only for crossing where the Y values are decreasing as *level* is crossed from wave start towards wave end.</td></tr></tbody></table>
| <span class="table-cell-nowrap">/M = *minWidthX*</span> | Sets the minimum X distance between level crossings. This determines where FindLevels searches for the next crossing after it has found a level crossing. The search starts *minWidthX* X units beyond the crossing. The default value for *minWidthX* is 0. |
| <span class="table-cell-nowrap">/N = *maxLevels*</span> | Sets a maximum number of crossings that FindLevels is to find. The default value for *maxLevels* is the number of points in the specified range of *waveName*. |
| <span class="table-cell-nowrap">/P</span> | Computes crossings in terms of points. See the [FindLevel](/igorpro/commands/findlevel.md) operation. |
| <span class="table-cell-nowrap">/Q</span> | Doesn't print to history and doesn't abort if no levels are found. See the [FindLevel](/igorpro/commands/findlevel.md) operation. |
| <span class="table-cell-nowrap">/R = (*startX*,*endX* )</span> | Specifies X range. See the [FindLevel](/igorpro/commands/findlevel.md) operation. |
| <span class="table-cell-nowrap">/R = [*startP*,*endP* ]</span> | Specifies point range. See the [FindLevel](/igorpro/commands/findlevel.md) operation. |
| <span class="table-cell-nowrap">/T = *dx*</span> | Searches for two level crossings. *dx* must be less than *minWidthX*, so you must also specify /M if you use /T. (FindLevels limits *dx* so that second search start isn't beyond where the first search for next edge will be.) See [FindLevel](/igorpro/commands/findlevel.md) for more about /T. |

### *Details* {#details}
The algorithm for finding a level crossing is the same one used by the [FindLevel](/igorpro/commands/findlevel.md) operation.

If FindLevels finds *maxLevels* crossings or cannot find another level crossing, it stops searching.

FindLevels sets the following variables:

|  |  |
| --- | --- |
| V_flag |<table class="nested-table"><tbody><tr><td>0:</td><td>*maxLevels* level crossings were found.</td></tr><tr><td>1:</td><td>At least one but less than *maxLevels* level crossings found.</td></tr><tr><td>2:</td><td>No level crossings were found.</td></tr></tbody></table>
| V_LevelsFound | Number of level crossings found. |

### *Example* {#example}

```igor
Macro FindLevelsExample()
	// Sample data
	Make/O/N=1024 peaks;SetScale/P x,0,0.001,"" peaks // 1ms sampling
	peaks=(exp(sawtooth(-(x-1)*300/pi)^3)-1)/(exp(1)-1)
	SetRandomSeed 0; peaks += gnoise(0.05)
	
	// locate rising and falling x crossings of y = 0.5
	Variable minDX=20*deltax(peaks) // min 20 samples between crossings
	Variable level = 0.5 // peaks y range nominally 0..1
	FindLevels/Q/D=risingEdges/EDGE=1/M=(minDX) peaks, level
	FindLevels/Q/D=fallingEdges/EDGE=2/M=(minDX) peaks, level

	// Indicate found edges
	Duplicate/O risingEdges, risingYs; risingYs = peaks(risingEdges[p])
	Duplicate/O fallingEdges, fallingYs; fallingYs = peaks(fallingEdges[p])
	// show level
	Make/O/N=2 showLevel = level;CopyScales/I peaks, showLevel
	
	Display /W=(35.25,41,856.5,249.5) peaks
	AppendToGraph risingYs vs risingEdges
	AppendToGraph fallingYs vs fallingEdges
	AppendToGraph showLevel
	ModifyGraph mode(risingYs)=8,mode(fallingYs)=8
	ModifyGraph marker(risingYs)=17,marker(fallingYs)=23
	ModifyGraph lStyle(showLevel)=1
	ModifyGraph rgb(risingYs)=(19675,39321,1),rgb(fallingYs)=(0,0,0),rgb(showLevel)=(1,16019,65535)
	Legend/C/N=text0/X=3.55/Y=1.90
End
```

### *See Also* {#see-also}
[FindLevel](/igorpro/commands/findlevel.md) for details about the level crossing detection algorithm and the /B, /P, /Q, /R, and /T flag values.

The FindLevels operation is not multidimensional aware. See [Multidimensional Waves](/igorpro/igor-basics/multidimensional-waves.md), particularly [Analysis on Multidimensional Waves](/igorpro/igor-basics/multidimensional-waves.md#analysis-on-multidimensional-waves) for details.