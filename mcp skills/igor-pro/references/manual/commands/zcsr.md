---
description: "The zcsr function returns a Z value when the specified cursor is on a contour, image or waterfall plot. Otherwise, it returns NaN."
slug: /commands/zcsr
---

<div className="command-signature">

## <strong>zcsr</strong> (<em>cursorName</em> [, <em>graphNameStr</em>]) {#zcsr}

</div>

The zcsr function returns a Z value when the specified cursor is on a contour, image or waterfall plot. Otherwise, it returns NaN.

### *Parameters* {#parameters}
*cursorName* identifies the cursor, which can be cursor *A* or *B*.

*graphNameStr* specifies the graph window or subwindow.

When identifying a subwindow with *graphNameStr*, see [Subwindow Syntax](/igorpro/graphing/making-figures/subwindows.md#subwindow-syntax) for details on forming the window hierarchy.

### *Examples* {#examples}

```igor
Print zcsr(A)           // not zcsr("A")
Print zcsr(A,"Graph0")  // specifies the graph
```

### *See Also* {#see-also}
[pcsr](/igorpro/commands/pcsr.md), [qcsr](/igorpro/commands/qcsr.md), [hcsr](/igorpro/commands/hcsr.md), [vcsr](/igorpro/commands/vcsr.md), [xcsr](/igorpro/commands/xcsr.md)

[Programming With Cursors](/igorpro/graphing/graphs.md#programming-with-cursors)