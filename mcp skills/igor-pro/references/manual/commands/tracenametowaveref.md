---
description: "The TraceNameToWaveRef function returns a wave reference to the Y wave corresponding to the given trace in the graph window or subwindow named by graphNameStr."
slug: /commands/tracenametowaveref
---

<div className="command-signature">

## <strong>TraceNameToWaveRef</strong> (<em>graphNameStr</em>, <em>traceNameStr</em>) {#tracenametowaveref}

</div>

The TraceNameToWaveRef function returns a wave reference to the Y wave corresponding to the given trace in the graph window or subwindow named by *graphNameStr*.

### *Parameters* {#parameters}
*graphNameStr* can be "" to refer to the top graph window.

When identifying a subwindow with *graphNameStr*, see [Subwindow Syntax](/igorpro/graphing/making-figures/subwindows.md#subwindow-syntax) for details on forming the window hierarchy.

The trace is identified by the string in *traceNameStr*, which could be a string determined using [TraceNameList](/igorpro/commands/tracenamelist.md). Note that the same trace name can refer to different waves in different graphs.

Use [Instance Notation](/igorpro/programming/commands.md#instance-notation) to choose from traces in a graph that represent waves of the same name. For example, if *traceNameStr* is "myWave#2", it refers to the third instance of a wave named "myWave" in the graph ("myWave#0" or just "myWave" is the first instance).

### *See Also* {#see-also}
[Trace Names](/igorpro/graphing/graphs.md#trace-names), [Programming With Trace Names](/igorpro/programming/programming.md#programming-with-trace-names)

For other commands related to waves and traces: [WaveRefIndexed](/igorpro/commands/waverefindexed.md), [XWaveRefFromTrace](/igorpro/commands/xwavereffromtrace.md), [TraceNameList](/igorpro/commands/tracenamelist.md), [CsrWaveRef](/igorpro/commands/csrwaveref.md), [CsrXWaveRef](/igorpro/commands/csrxwaveref.md).

For a description of wave references: [Wave Reference Functions](/igorpro/programming/programming-techniques.md#wave-reference-functions).

For a description of Traces: [ModifyGraph](/igorpro/commands/modifygraph.md).

For a discussion of Contour Traces: [Contour Traces](/igorpro/graphing/contour-plots.md#contour-traces).

For commands referencing other waves in a graph: [ImageNameList](/igorpro/commands/imagenamelist.md), [ImageNameToWaveRef](/igorpro/commands/imagenametowaveref.md), [ContourNameList](/igorpro/commands/contournamelist.md), [ContourNameToWaveRef](/igorpro/commands/contournametowaveref.md).

### *See Also* {#tracenametowaveref-see-also}
[Trace Names](/igorpro/graphing/graphs.md#trace-names), [Programming With Trace Names](/igorpro/programming/programming.md#programming-with-trace-names)