---
description: "The RemoveFromGraph operation removes the specified wave traces from the target or named graph."
slug: /commands/removefromgraph
---

<div className="command-signature">

## <strong>RemoveFromGraph</strong>  [/ALL /W=<em>winName</em> /Z] <em>traceName</em> [,<em>traceName</em> ]... {#removefromgraph}

</div>

The RemoveFromGraph operation removes the specified wave traces from the target or named graph. A trace is a representation of the data in a wave, usually connected line segments.

### *Parameters* {#parameters}
*traceName* is usually just the name of a wave.

More generally, *traceName* is a wave name, optionally followed by the # character and an instance number - for example, wave0#1. See [Instance Notation](/igorpro/programming/commands.md#instance-notation) for details.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/ALL</span> | Removes all non-contour traces from the graph. Any trace name parameters listed are ignored. /ALL was added in Igor Pro 9.00. |
| <span class="table-cell-nowrap">/W = *winName*</span> | Removes traces from the named graph window or subwindow. When omitted, action will affect the active window or subwindow. This must be the first flag specified when used in a Proc or Macro or on the command line. |
|  | When identifying a subwindow with *winName*, see [Subwindow Syntax](/igorpro/graphing/making-figures/subwindows.md#subwindow-syntax) for details on forming the window hierarchy. |
| <span class="table-cell-nowrap">/Z</span> | Suppresses error if specified trace or image is not on the graph. |

### *Details* {#details}
Up to 100 *traceNames* may be specified, subject to the 2500 byte command length limit.

A string containing *traceName* can be used with the $ operator to specify *traceName*.

Specifying $"#0" for *traceName* removes the first trace in the graph. $"#1" removes the second trace in the graph, and so on. $"" is equivalent to $"#0".

Note that removing all the contour traces from a contour plot is not the same as removing the contour plot itself. Use the [RemoveContour](/igorpro/commands/removecontour.md) operation.

### *Examples* {#examples}
The command:


```igor
Display myWave,myWave;Modify mode(myWave#1)=6
```

appends two instances of myWave to the graph.The first/backmost instance of myWave is instance 0, and its trace name is just "myWave" as a synonym for "myWave#0". The second/frontmost wave instance of myWave is "myWave#1" and it is displayed with the cityscape mode.

To remove the second instance from the graph requires the command:


```igor
RemoveFromGraph myWave#1
```

or


```igor
String MyTraceName="myWave#1"
RemoveFromGraph $MyTraceName
```

### *See Also* {#see-also}
[Trace Names](/igorpro/graphing/graphs.md#trace-names), [Programming With Trace Names](/igorpro/programming/programming.md#programming-with-trace-names)