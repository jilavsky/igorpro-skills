---
description: "The TraceNameList function returns a string containing a list of traces in the graph window or subwindow identified by graphNameStr."
slug: /commands/tracenamelist
---

<div className="command-signature">

## <strong>TraceNameList</strong> (<em>graphNameStr</em>, <em>separatorStr</em>, <em>optionsFlag</em>) {#tracenamelist}

</div>

The TraceNameList function returns a string containing a list of traces in the graph window or subwindow identified by *graphNameStr*.

### *Parameters* {#parameters}
*graphNameStr* can be "" to refer to the top graph.

When identifying a subwindow with *graphNameStr*, see [Subwindow Syntax](/igorpro/graphing/making-figures/subwindows.md#subwindow-syntax) for details on forming the window hierarchy.

The parameter *separatorStr* should contain a single ASCII character such as "," or ";" to separate the names.

### *Details* {#details}
The bits of *optionsFlag* have the following meanings:

|  |  |
| --- | --- |
| Bit 0: | Include normal graph traces |
| Bit 1: | Include contour traces |
| Bit 2: | Omit hidden traces (the default is to list even hidden traces) |
| Bit 3: | Include box plot traces |
| Bit 4: | Include violin plot traces |

See [Setting Bit Parameters](/igorpro/programming/commands.md#setting-bit-parameters) for details about bit settings.

A trace name is defined as the name of the Y wave that defines the trace with an optional #ddd suffix that distinguishes between two or more traces that have the same wave name. It may also be a user-defined trace name. Since the trace name must be parsed, it is quoted if necessary..

Commands that take a trace name as a parameter or in a keyword can use a string containing a trace name with the $ operator to specify *traceName*. For instance, to change the display mode of a wave, you might use


```igor
ModifyGraph mode(myWave#1)=3
```

but


```igor
String myTraceName="myWave#1"
ModifyGraph mode($myTraceName)=3
```

will also work.

### *Examples* {#examples}

```igor
Make/O jack,'jack # 2';Display jack,jack,'jack # 2','jack # 2'
Print TraceNameList("",";",1)

// Prints: jack;jack#1;'jack # 2';'jack # 2'#1;
// Generate a list of hidden traces
Make/O jack,jill,joy;Display jack,jill,joy
ModifyGraph hideTrace(joy)=1		// hide joy

// (hidden + visible) - visible = hidden
String visibleTraces=TraceNameList("",";",1+4)  // only visible normal traces
String allNormalTraces=TraceNameList("",";",1)  // hidden + visible normal traces
String hiddenTraces= RemoveFromList(visibleTraces,allNormalTraces)
Print hiddenTraces
// Prints: joy;
```

### *See Also* {#see-also}
[Trace Names](/igorpro/graphing/graphs.md#trace-names), [Programming With Trace Names](/igorpro/programming/programming.md#programming-with-trace-names), [User-defined Trace Names](/igorpro/programming/programming.md#user-defined-trace-names)

For other commands related to waves and traces: [WaveRefIndexed](/igorpro/commands/waverefindexed.md), [XWaveRefFromTrace](/igorpro/commands/xwavereffromtrace.md), [TraceNameToWaveRef](/igorpro/commands/tracenametowaveref.md), [CsrWaveRef](/igorpro/commands/csrwaveref.md), [CsrXWaveRef](/igorpro/commands/csrxwaveref.md), [StringFromList](/igorpro/commands/stringfromlist.md).

For a description of wave references: [Wave Reference Functions](/igorpro/programming/programming-techniques.md#wave-reference-functions).

For a description of Traces: [ModifyGraph](/igorpro/commands/modifygraph.md).

For a discussion of Contour Traces: [Contour Traces](/igorpro/graphing/contour-plots.md#contour-traces).

For commands referencing other waves in a graph: [ImageNameList](/igorpro/commands/imagenamelist.md), [ImageNameToWaveRef](/igorpro/commands/imagenametowaveref.md), [ContourNameList](/igorpro/commands/contournamelist.md), [ContourNameToWaveRef](/igorpro/commands/contournametowaveref.md).