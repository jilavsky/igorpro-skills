---
description: "The vcsr function returns the Y (vertical) value of the point which the specified cursor (A through J) is attached to in the top (or named) graph."
slug: /commands/vcsr
---

<div className="command-signature">

## <strong>vcsr</strong> (<em>cursorName</em> [, <em>graphNameStr</em>]) {#vcsr}

</div>

The vcsr function returns the Y (vertical) value of the point which the specified cursor (A through J) is attached to in the top (or named) graph.

### *Parameters* {#parameters}
*cursorName* identifies the cursor, which can be cursor A through J.

*graphNameStr* specifies the graph window or subwindow.

When identifying a subwindow with *graphNameStr*, see [Subwindow Syntax](/igorpro/graphing/making-figures/subwindows.md#subwindow-syntax) for details on forming the window hierarchy.

### *Details* {#details}
The result is computed from the coordinate system of the graph's Y axis. The Y axis used is the one used to display the wave on which the cursor is placed.

### *See Also* {#see-also}
[pcsr](/igorpro/commands/pcsr.md), [qcsr](/igorpro/commands/qcsr.md), [hcsr](/igorpro/commands/hcsr.md), [xcsr](/igorpro/commands/xcsr.md), [zcsr](/igorpro/commands/zcsr.md)

[Programming With Cursors](/igorpro/graphing/graphs.md#programming-with-cursors)