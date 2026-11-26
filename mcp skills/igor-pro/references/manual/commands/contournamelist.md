---
description: "The ContourNameList function returns a string containing a list of contour names in the graph window or subwindow identified by graphNameStr."
slug: /commands/contournamelist
---

<div className="command-signature">

## <strong>ContourNameList</strong> (<em>graphNameStr</em>, <em>separatorStr</em> ) {#contournamelist}

</div>

The ContourNameList function returns a string containing a list of contour names in the graph window or subwindow identified by *graphNameStr.*

### *Parameters* {#parameters}
*graphNameStr*  can be "" to refer to the top graph.

When identifying a subwindow with *graphNameStr*, see [Subwindow Syntax](/igorpro/graphing/making-figures/subwindows.md#subwindow-syntax) for details on forming the window hierarchy.

The parameter *separatorStr* should contain a single ASCII character such as "," or ";" to separate the names.

An contour name is defined as the name of the 2D wave containing the data from which a contour plot is calculated, with an optional #n suffix that distinguishes between two or more contour plots in the same graph window that have the same wave name. Since the contour name has to be parsed, it is quoted if necessary.

### *Examples* {#examples}
The following command lines create a very unlikely contour display. If you did this, you would most likely want to put each contour plot on different axes, and arrange the axes such that they don't overlap. That would greatly complicate the example.


```igor
Make/O/N=(20,20) jack,'jack # 2';
Display;AppendMatrixContour jack
AppendMatrixContour/T/R jack
AppendMatrixContour 'jack # 2'
AppendMatrixContour/T/R 'jack # 2'
Print ContourNameList("",";")
```

prints  jack;jack#1;'jack # 2';'jack # 2'#1;

### *See Also* {#see-also}
Another command related to contour plots and waves: [ContourNameToWaveRef](/igorpro/commands/contournametowaveref.md).

For a description of wave references: [Wave Reference Functions](/igorpro/programming/programming-techniques.md#wave-reference-functions).

For commands referencing other waves in a graph: [TraceNameList](/igorpro/commands/tracenamelist.md), [WaveRefIndexed](/igorpro/commands/waverefindexed.md), [XWaveRefFromTrace](/igorpro/commands/xwavereffromtrace.md), [TraceNameToWaveRef](/igorpro/commands/tracenametowaveref.md), [CsrWaveRef](/igorpro/commands/csrwaveref.md), [CsrXWaveRef](/igorpro/commands/csrxwaveref.md), [ImageNameList](/igorpro/commands/imagenamelist.md), [ImageNameToWaveRef](/igorpro/commands/imagenametowaveref.md).