---
description: "The XWaveRefFromTrace function returns a wave reference to the wave supplying the X coordinates against which the named trace is displayed in the named graph…"
slug: /commands/xwavereffromtrace
---

<div className="command-signature">

## <strong>XWaveRefFromTrace</strong> (<em>graphNameStr</em>, <em>traceNameStr</em>) {#xwavereffromtrace}

</div>

The XWaveRefFromTrace function returns a wave reference to the wave supplying the X coordinates against which the named trace is displayed in the named graph window or subwindow.

### *Parameters* {#parameters}
*graphNameStr* can be "" to refer to the top graph window.

When identifying a subwindow with *graphNameStr*, see [Subwindow Syntax](/igorpro/graphing/making-figures/subwindows.md#subwindow-syntax) for details on forming the window hierarchy.

### *Details* {#details}
XWaveRefFromTrace returns a null reference (see [WaveExists](/igorpro/commands/waveexists.md)) if the wave is not plotted versus an X wave.

*graphNameStr* and *traceNameStr* are strings, not names.

### *Examples* {#examples}

```igor
Display ywave vs xwave                  // XY graph
Print XWaveRefFromTrace("","ywave")[50] // prints xwave value at point 50
```

### *See Also* {#see-also}
[Trace Names](/igorpro/graphing/graphs.md#trace-names), [Programming With Trace Names](/igorpro/programming/programming.md#programming-with-trace-names)

For other commands related to waves and traces: [WaveRefIndexed](/igorpro/commands/waverefindexed.md), [TraceNameToWaveRef](/igorpro/commands/tracenametowaveref.md), [TraceNameList](/igorpro/commands/tracenamelist.md), [CsrWaveRef](/igorpro/commands/csrwaveref.md), [CsrXWaveRef](/igorpro/commands/csrxwaveref.md).

For a description of wave references: [Wave Reference Functions](/igorpro/programming/programming-techniques.md#wave-reference-functions).

For a description of Traces: [ModifyGraph](/igorpro/commands/modifygraph.md).

For a discussion of Contour Traces: [Contour Traces](/igorpro/graphing/contour-plots.md#contour-traces).

For commands referencing other waves in a graph: [ImageNameList](/igorpro/commands/imagenamelist.md), [ImageNameToWaveRef](/igorpro/commands/imagenametowaveref.md), [ContourNameList](/igorpro/commands/contournamelist.md), [ContourNameToWaveRef](/igorpro/commands/contournametowaveref.md).