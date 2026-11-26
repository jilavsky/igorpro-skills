---
description: "The qcsr function can be used with cursors on images or waterfall plots to return the column number."
slug: /commands/qcsr
---

<div className="command-signature">

## <strong>qcsr</strong> (<em>cursorName</em>  [, <em>graphNameStr</em> ]) {#qcsr}

</div>

The qcsr function can be used with cursors on images or waterfall plots to return the column number. It can also be used with free cursors to return the relative y coordinate.

### *Parameters* {#parameters}
*cursorName* identifies the cursor, which can be cursor *A* or *B*.

*graphNameStr* specifies the graph window or subwindow.

When identifying a subwindow with *graphNameStr*, see [Subwindow Syntax](/igorpro/graphing/making-figures/subwindows.md#subwindow-syntax) for details on forming the window hierarchy.

### *See Also* {#see-also}
[pcsr](/igorpro/commands/pcsr.md), [hcsr](/igorpro/commands/hcsr.md), [vcsr](/igorpro/commands/vcsr.md), [xcsr](/igorpro/commands/xcsr.md), [zcsr](/igorpro/commands/zcsr.md)

[Programming With Cursors](/igorpro/graphing/graphs.md#programming-with-cursors)