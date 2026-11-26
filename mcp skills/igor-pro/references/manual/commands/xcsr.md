---
description: "The xcsr function returns the X value of the point which the named cursor (A through J) is on in the top (or named) graph."
slug: /commands/xcsr
---

<div className="command-signature">

## <strong>xcsr</strong> (<em>cursorName</em> [, <em>graphNameStr</em>]) {#xcsr}

</div>

The xcsr function returns the X value of the point which the named cursor (A through J) is on in the top (or named) graph.

### *Parameters* {#parameters}
*cursorName* identifies the cursor, which can be cursor A through J.

*graphNameStr* specifies the graph window or subwindow.

When identifying a subwindow with *graphNameStr*, see [Subwindow Syntax](/igorpro/graphing/making-figures/subwindows.md#subwindow-syntax) for details on forming the window hierarchy.

### *Details* {#details}
The result is derived from the wave that the cursor is on, not from the X axis of the graph. If the wave is displayed as an XY pair, the X axis and the wave's X scaling will usually be different.

### *See Also* {#see-also}
[pcsr](/igorpro/commands/pcsr.md), [qcsr](/igorpro/commands/qcsr.md), [hcsr](/igorpro/commands/hcsr.md), [vcsr](/igorpro/commands/vcsr.md), [zcsr](/igorpro/commands/zcsr.md)

[Programming With Cursors](/igorpro/graphing/graphs.md#programming-with-cursors)