---
description: "The XWaveName function returns a string containing the name of the wave supplying the X coordinates for the named trace in the named graph window or subwindow."
slug: /commands/xwavename
---

<div className="command-signature">

## <strong>XWaveName</strong> (<em>graphNameStr</em>, <em>traceNameStr</em>) {#xwavename}

</div>

The XWaveName function returns a string containing the name of the wave supplying the X coordinates for the named trace in the named graph window or subwindow.

### *Parameters* {#parameters}
*graphNameStr* can be "" to refer to the top graph window.

When identifying a subwindow with *graphNameStr*, see [Subwindow Syntax](/igorpro/graphing/making-figures/subwindows.md#subwindow-syntax) for details on forming the window hierarchy.

*traceNameStr* is the name of the trace in question.

### *Details* {#details}
XWaveName returns an empty string ("") if the trace is not plotted versus an X wave.

For most uses, we recommend that you use [XWaveRefFromTrace](/igorpro/commands/xwavereffromtrace.md) instead of WaveName. XWaveName returns a string containing the wave name only, with no data folder path qualifying it. Thus, you may get erroneous results if the X wave referred to in the graph has the same name as a different wave in the current data folder. Likewise, if the named wave resides in a folder that is not the current data folder, you will not be able to refer to the named wave. Use [XWaveRefFromTrace](/igorpro/commands/xwavereffromtrace.md) instead.

*graphNameStr* and *traceNameStr* are strings, not names.

### *Examples* {#examples}

```igor
Display ywave vs xwave      // XY graph
Print XWaveName("","ywave") // prints xwave
```

### *See Also* {#see-also}
[Trace Names](/igorpro/graphing/graphs.md#trace-names), [Programming With Trace Names](/igorpro/programming/programming.md#programming-with-trace-names)