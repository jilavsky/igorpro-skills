---
description: "The ImageNameList function returns a string containing a list of image names in the graph window or subwindow identified by graphNameStr."
slug: /commands/imagenamelist
---

<div className="command-signature">

## <strong>ImageNameList</strong> (<em>graphNameStr</em>, <em>separatorStr</em>) {#imagenamelist}

</div>

The ImageNameList function returns a string containing a list of image names in the graph window or subwindow identified by *graphNameStr*.

### *Parameters* {#parameters}
*graphNameStr* can be "" to refer to the top graph.

When identifying a subwindow with *graphNameStr*, see [Subwindow Syntax](/igorpro/graphing/making-figures/subwindows.md#subwindow-syntax) for details on forming the window hierarchy.

The parameter *separatorStr* should contain a single ASCII character such as "," or ";" to separate the names.

An image name is defined as the name of the 2D wave that defines the image with an optional #ddd suffix that distinguishes between two or more images that have the same wave name. Since the image name has to be parsed, it is quoted if necessary.

### *Examples* {#examples}
The following command lines create a very unlikely image display. If you did this, you would want to put each image on different axes, and arrange the axes such that they don't overlap. That would greatly complicate the example.


```igor
Make/O/N=(20,20) jack,'jack # 2';
Display;AppendImage jack
AppendImage/T/R jack
AppendImage 'jack # 2'
AppendImage/T/R 'jack # 2'
Print ImageNameList("",";")
```

prints  jack;jack#1;'jack # 2';'jack # 2'#1;

### *See Also* {#see-also}
Another command related to images and waves: [ImageNameToWaveRef](/igorpro/commands/imagenametowaveref.md).

For a description of wave references: [Wave Reference Functions](/igorpro/programming/programming-techniques.md#wave-reference-functions).

For commands referencing other waves in a graph: [TraceNameList](/igorpro/commands/tracenamelist.md), [WaveRefIndexed](/igorpro/commands/waverefindexed.md), [XWaveRefFromTrace](/igorpro/commands/xwavereffromtrace.md), [TraceNameToWaveRef](/igorpro/commands/tracenametowaveref.md), [CsrWaveRef](/igorpro/commands/csrwaveref.md), [CsrXWaveRef](/igorpro/commands/csrxwaveref.md), [ContourNameList](/igorpro/commands/contournamelist.md), [ContourNameToWaveRef](/igorpro/commands/contournametowaveref.md).