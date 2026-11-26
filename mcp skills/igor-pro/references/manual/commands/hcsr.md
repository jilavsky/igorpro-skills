---
description: "The hcsr function returns the horizontal coordinate of the named cursor (A through J) in the coordinate system of the top (or named) graph's X axis."
slug: /commands/hcsr
---

<div className="command-signature">

## <strong>hcsr</strong> (<em>cursorName</em> [, <em>graphNameStr</em>]) {#hcsr}

</div>

The hcsr function returns the horizontal coordinate of the named cursor (A through J) in the coordinate system of the top (or named) graph's X axis.

### *Parameters* {#parameters}
*cursorName* identifies the cursor, which can be cursor A through J.

*graphNameStr* specifies the graph window or subwindow.

When identifying a subwindow with *graphNameStr*, see [Subwindow Syntax](/igorpro/graphing/making-figures/subwindows.md#subwindow-syntax) for details on forming the window hierarchy.

### *Details* {#details}
The X axis used is the one that controls the trace on which the cursor is placed.

### *Examples* {#examples}

```igor
Variable xAxisValueAtCursorA = hcsr(A)  // not hcsr("A")
String str="A"
Variable xA= hcsr($str,"Graph0")        // $str is a name, too
```

### *See Also* {#see-also}
[pcsr](/igorpro/commands/pcsr.md), [qcsr](/igorpro/commands/qcsr.md), [vcsr](/igorpro/commands/vcsr.md), [xcsr](/igorpro/commands/xcsr.md), [zcsr](/igorpro/commands/zcsr.md)

[Programming With Cursors](/igorpro/graphing/graphs.md#programming-with-cursors)