---
description: "The ReorderTraces operation changes the ordering of graph traces to that specified in the braces."
slug: /commands/reordertraces
---

<div className="command-signature">

## <strong>ReorderTraces</strong>  [/W=<em>winName</em>  /L[=<em>axisName</em>] /R[=<em>axisName</em>]] <em>anchorTrace</em>, {<em>traceA</em>, <em>traceB</em>,...} {#reordertraces}

</div>

The ReorderTraces operation changes the ordering of graph traces to that specified in the braces.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/W = *winName*</span> | Reorders traces in the named graph window or subwindow. When omitted, action will affect the active window or subwindow. This must be the first flag specified when used in a Proc or Macro or on the command line. |
|  | When identifying a subwindow with *winName*, see [Subwindow Syntax](/igorpro/graphing/making-figures/subwindows.md#subwindow-syntax) for details on forming the window hierarchy. |
| <span class="table-cell-nowrap">/L [ = *axisName*]</span> |  |
| <span class="table-cell-nowrap">/R [ = *axisName*]</span> | Moves traces to a new or existing axis. This feature was added in Igor Pro 8.00. |
|  | To reference the built-in left or right axes, you can use /L or /R without specifying the axis name. To reference a free axis, you must specify the axis name. |
|  | If the specified axis does not already exist, a new axis is created by cloning the axis controlling *traceA*. |
|  | If the move results in no traces assigned to an axis, then that axis is deleted. |
|  | Reordering is optional. Specify \_none\_ for *anchorTrace* for no reordering. |
|  | You can move a trace manually by right-clicking a trace and choosing Move to Opposite Axis. |

### *Details* {#details}
Igor keeps a list of traces in a graph and draws the traces in the listed order. The first trace drawn is consequently at the bottom. All other traces are drawn on top of it. The last trace is the top one; no other trace obscures it.

ReorderTraces works by removing the traces in the braces from the list and then reinserting them at the location specified by *anchorTrace*. If *anchorTrace* is not in the braces, the traces in braces are placed before *anchorTrace*.

If the list of traces is A, B, C, D, E, F, G and you execute the command


```igor
ReorderTraces F, {B,C}
```

traces B and C are placed just before F: A, D, E, **B**,  **C**,  F, G. The result of


```igor
ReorderTraces E, {D,E,C}
```

is to reorder C, D and E and put them where E was. Starting from the initial ordering results in A, B, **D**, **E**, **C**, F, G.

ReorderTraces generates an error if the same trace is in the list twice.

In Igor 7 or later, *anchorTrace* can be \_front\_ or \_back\_. To move A to the front, you can write:


```igor
ReorderTraces _front_, {A}
```

### *See Also* {#see-also}
[Trace Names](/igorpro/graphing/graphs.md#trace-names), [Programming With Trace Names](/igorpro/programming/programming.md#programming-with-trace-names)

[ReorderImages](/igorpro/commands/reorderimages.md)