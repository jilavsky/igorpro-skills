---
description: "The MoveSubwindow operation moves the active or named subwindow to a new location within the host window."
slug: /commands/movesubwindow
---

<div className="command-signature">

## <strong>MoveSubwindow</strong>  [/W=<em>winName</em> ] [<em>fguide</em>=(<em>gLeft</em>, <em>gTop</em>, <em>gRight</em>, <em>gBottom</em> ), <em>fnum</em>=(<em>left</em>, <em>top</em>, <em>right</em>, <em>bottom</em> ), <em>pguide</em>=(<em>gLeft</em>, <em>gTop</em>, <em>gRight</em>, <em>gBottom</em> )] {#movesubwindow}

</div>

The MoveSubwindow operation moves the active or named subwindow to a new location within the host window. This command is primarily for use in recreation macros; users should use layout mode for repositioning subwindows.

### *Parameters* {#parameters}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">fguide = (*gLeft*, *gTop*, *gRight*, *gBottom* )</span> |  |
|  | Specifies the frame guide name(s) to which the outer frame of the subwindow is attached inside the host window. |
|  | The frame guides are identified by the standard names or user-defined names as defined by the host. Use * to specify a default guide name. |
|  | When the host is a graph, additional standard guides are available for the outer graph rectangle and the inner plot rectangle (where traces are plotted). |
|  | See Details below for standard guide names. |
| <span class="table-cell-nowrap">fnum = (*left*, *top*, *right*, *bottom* )</span> |  |
|  | Specifies the new location of the subwindow. The location coordinates of the subwindow sides can have one of two possible meanings: |
|  |<table class="nested-table"><tbody><tr><td>1.</td><td>When all values are less than 1, coordinates are assumed to be fractional relative to the host frame size.</td></tr><tr><td>2.</td><td>When any value is greater than 1, coordinates are taken to be fixed locations measured in points, or [control panel units](/igorpro/user-interface/controls.md#control-panel-units) for control panel hosts, relative to the top left corner of the host frame.</td></tr></tbody></table>
| <span class="table-cell-nowrap">pguide = (*gLeft*, *gTop*, *gRight*, *gBottom* )</span> |  |
|  | Specifies the guide name(s) to which the plot rectangle of the graph subwindow is attached inside the host window. |
|  | Guides are identified by the standard names or user-defined names as defined by the host. Use \* to specify a default guide name. |
|  | See Details below for standard guide names. |

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/W = *winName*</span> | Moves the subwindow in the named window or subwindow. When omitted, action will affect the active subwindow. |
|  | When identifying a subwindow with *winName*, see [Subwindow Syntax](/igorpro/graphing/making-figures/subwindows.md#subwindow-syntax) for details on forming the window hierarchy. |

### *Details* {#details}
When moving an exterior subwindow, only the fnum keyword may be used. The values are the same as the [NewPanel](/igorpro/commands/newpanel.md) /W flag for exterior subwindows.

The names for the built-in guides are as defined in the following table:

| Guide Names | Left | Right | Top | Bottom |
| --- | --- | --- | --- | --- |
| Subwindow Frame | FL | FR | FT | FB |
| Outer Graph Rectangle | GL | GR | GT | GB |
| Inner Plot Rectangle | PL | PR | PT | PB |

The frame guides apply to all window and subwindow types. The graph rectangle and plot rectangle guide types apply only to graph windows and subwindows.

### *See Also* {#see-also}
[MoveWindow](/igorpro/commands/movewindow.md), [Embedding and Subwindows](/igorpro/graphing/making-figures/subwindows.md)