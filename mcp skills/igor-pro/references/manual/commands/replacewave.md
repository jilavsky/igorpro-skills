---
description: "The ReplaceWave operation replaces waves displayed in a graph with other waves."
slug: /commands/replacewave
---

<div className="command-signature overload">

## <strong>ReplaceWave</strong>  [/W=<em>winName</em> ] <em>allinCDF</em> {#replacewave}

</div>
<div className="command-signature overload">

## <strong>ReplaceWave</strong>  [/X/W=<em>winName</em> ] <em>trace</em>=<em>traceName</em> , <em>waveName</em> {#replacewave}

</div>
<div className="command-signature overload">

## <strong>ReplaceWave</strong>  [/X/Y/W=<em>winName</em> ] <em>image</em>=<em>imageName</em> , <em>waveName</em> {#replacewave}

</div>
<div className="command-signature">

## <strong>ReplaceWave</strong>  [/X/Y/W=<em>winName</em> ] <em>contour</em>=<em>contourName</em> , <em>waveName</em> {#replacewave}

</div>

The ReplaceWave operation replaces waves displayed in a graph with other waves. The waves to be replaced, and the replacement waves are chosen by the flags, the keyword and the wave names on the command line.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/W = *winName*</span> | Replaces the wave in the named graph window or subwindow. When omitted, action will affect the active window or subwindow. |
|  | When identifying a subwindow with *winName*, see [Subwindow Syntax](/igorpro/graphing/making-figures/subwindows.md#subwindow-syntax) for details on forming the window hierarchy. |
| <span class="table-cell-nowrap">/X</span> | Replaces the wave supplying X coordinates. |
|  | If the trace represents a category plot, the wave must be either a text wave or the special keyword '\_labels\_' to use dimension labels from the Y wave controlling the axis. |
| <span class="table-cell-nowrap">/Y</span> | Replaces the wave supplying Y data. |

### *Keywords* {#keywords}

|  |  |
| --- | --- |
| allinCDF | Searches the current data folder for waves with the same names as waves used in the graph. If found and if the waves are of the correct type, they replace the existing waves. Thus, if you have several data folders with identically-named waves containing data from different experimental runs, you can browse through the runs by moving from one data folder to another, using ReplaceWave allinCDF to update the graph. |
| <span class="table-cell-nowrap">contour = *contourName*</span> | Replaces the wave supplying the Z data for *contourName*. If /X or /Y is used, replaces the wave used to set the X or Y data spacing (if the Z data are in a matrix) or the wave used to supply the X or Y positions if XYZ triplets were specified with three separate waves. |
| <span class="table-cell-nowrap">image = *imageName*</span> | Replaces the wave supplying the Z data for *imageName*. If /X or /Y is used, replaces the wave used to set the X or Y data spacing. |
| <span class="table-cell-nowrap">trace = *traceName*</span> | Replaces the wave associated with *traceName*. The wave supplying Y values will be replaced with *waveName*. Use the /X flag to replace the X wave associated with *traceName*. Note that *traceName* is derived from the Y wave name. If you create a graph using: |
|  | <code class="igor">Display jack vs sam</code> |
|  | To replace the X wave, you would use: |
|  | <code class="igor">ReplaceWave/X trace=jack, newsam</code> |
|  | For traces, ReplaceWave/Y is equivalent to ReplaceWave with no flags. |

### *Details* {#details}
Waves are replaced in the graph specified by /W=*winName*. If the /W flag is not present, waves are replaced in the top graph.

Updating a contour plot in response to replacing a wave can be time-consuming. If you must replace more than one wave, put all the commands separated by semicolons on a single line. In a macro, use [DelayUpdate](/igorpro/commands/delayupdate.md) to prevent updates between command lines.

When using the allinCDF keyword, ReplaceWave cannot find waves buried in dynamic annotation text (for instance, using the \{} syntax in an annotation). ReplaceWave will not replace waves used for error bars, either.

Subsets of data, including individual rows or columns from a matrix, may be specified using [Subrange Display Syntax](/igorpro/graphing/graphs.md#subrange-display-syntax).

### *Examples* {#examples}
Make XY plot, then replace the waves:


```igor
Make fred=x, sam=log(x)
Display fred vs sam
Make fred2=2*x, sam2=ln(x)
ReplaceWave/X trace=fred, sam2
ReplaceWave trace=fred, fred2	// trace is now named fred2
```

Make contour plot with XYZ triplet waves, then replace the waves. Note the DelayUpdate commands after the first two ReplaceWave commands:


```igor
Make/N=100 junkx, junky, junkz                      // Waves for XYZ triplets
junkx=trunc(x/10)                                   // X wave for XYZ triplets
junky=mod(x,10)                                     // Y wave for XYZ triplets
junkz=sin(junkx[p])*cos(junky[p])                   // Z wave for XYZ triplets
Display; AppendXYZContour junkz vs {junkx, junky}   // Make contour plot
Make/O/N=150 junkx2, junky2, junkz2                 // Make replacement waves
junkx2=trunc(x/15)
junky2=mod(x,15)
junkz2=sin(junkx2[p])*cos(junky2[p])
ReplaceWave/X contour=junkz,junkx2; DelayUpdate
ReplaceWave/Y contour=junkz,junky2; DelayUpdate
ReplaceWave contour=junkz,junkz2
```

This example is suitable for copying all the lines and pasting into the command line, or for use in a macro. If you are typing on the command line, you would want to put the ReplaceWave commands all on one line:


```igor
ReplaceWave/X contour=junkz,junkx2;ReplaceWave/Y contour=junkz,junky2;...
```

### *See Also* {#see-also}
[Trace Names](/igorpro/graphing/graphs.md#trace-names), [Programming With Trace Names](/igorpro/programming/programming.md#programming-with-trace-names)