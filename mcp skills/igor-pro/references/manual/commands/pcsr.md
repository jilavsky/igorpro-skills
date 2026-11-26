---
description: "The pcsr function returns the point number of the point which the specified cursor (A through J) is on in the top (or named) graph."
slug: /commands/pcsr
---

<div className="command-signature">

## <strong>pcsr</strong> (<em>cursorName</em> [, <em>graphNameStr</em>]) {#pcsr}

</div>

The pcsr function returns the point number of the point which the specified cursor (A through J) is on in the top (or named) graph. When used with cursors on images or waterfall plots, pcsr returns the row number and when used with a free cursor, it returns the relative x coordinate.

### *Parameters* {#parameters}
*cursorName* identifies the cursor, which can be cursor A through J.

*graphNameStr* specifies the graph window or subwindow.

When identifying a subwindow with *graphNameStr*, see [Subwindow Syntax](/igorpro/graphing/making-figures/subwindows.md#subwindow-syntax) for details on forming the window hierarchy.

### *Details* {#details}
The pcsr result is not affected by any X axis.

### *See Also* {#see-also}
[qcsr](/igorpro/commands/qcsr.md), [hcsr](/igorpro/commands/hcsr.md), [vcsr](/igorpro/commands/vcsr.md), [xcsr](/igorpro/commands/xcsr.md), [zcsr](/igorpro/commands/zcsr.md)

[Programming With Cursors](/igorpro/graphing/graphs.md#programming-with-cursors)